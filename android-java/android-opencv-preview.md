# Android Opencv Preview 방향전환 문제

CameraBridgeViewBase 파일을 수정해야한다.

```java
public CameraBridgeViewBase(Context context, int cameraId) {  
   super(context);  
   mCameraIndex = cameraId;  
   getHolder().addCallback(this);  
   mMaxWidth = MAX_UNSPECIFIED;  
   mMaxHeight = MAX_UNSPECIFIED;  
   windowManager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);  
```

```java
public CameraBridgeViewBase(Context context, AttributeSet attrs) {  
   super(context, attrs);  
   int count = attrs.getAttributeCount();  
   Log.d(TAG, "Attr count: " + Integer.valueOf(count));  

   TypedArray styledAttrs = getContext().obtainStyledAttributes(attrs, R.styleable.CameraBridgeViewBase);  
   if (styledAttrs.getBoolean(R.styleable.CameraBridgeViewBase_show_fps, false))  
       enableFpsMeter();  

   mCameraIndex = styledAttrs.getInt(R.styleable.CameraBridgeViewBase_camera_id, -1);  

   getHolder().addCallback(this);  
   mMaxWidth = MAX_UNSPECIFIED;  
   mMaxHeight = MAX_UNSPECIFIED;  
   windowManager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);  
   styledAttrs.recycle();  
```

deliverAndDrawFrame 메소드를 아래와 같이 변경해야한다.

```java
protected void deliverAndDrawFrame(CvCameraViewFrame frame) {  
  Mat modified;  

  if (mListener != null) {  
      modified = mListener.onCameraFrame(frame);  
  } else {  
      modified = frame.rgba();  
  }  

  boolean bmpValid = true;  
  if (modified != null) {  
      try {  
          Utils.matToBitmap(modified, mCacheBitmap);  
      } catch (Exception e) {  
          Log.e(TAG, "Mat type: " + modified);  
          Log.e(TAG, "Bitmap type: " + mCacheBitmap.getWidth() + "*" + mCacheBitmap.getHeight());  
          Log.e(TAG, "Utils.matToBitmap() throws an exception: " + e.getMessage());  
          bmpValid = false;  
      }  
  }  

  if (bmpValid && mCacheBitmap != null) {  
      Canvas canvas = getHolder().lockCanvas();  
      if (canvas != null) {  
          canvas.drawColor(0, android.graphics.PorterDuff.Mode.CLEAR);  
          int rotation = windowManager.getDefaultDisplay().getRotation();  
          int degrees = 0;  
          // config degrees as you need  
          switch (rotation) {  
              case Surface.ROTATION_0:  
                  degrees = 90;  
                  break;  
              case Surface.ROTATION_90:  
                  degrees = 0;  
                  break;  
              case Surface.ROTATION_180:  
                  degrees = 270;  
                  break;  
              case Surface.ROTATION_270:  
                  degrees = 180;  
                  break;  
          }  

          Matrix matrix = new Matrix();  
          matrix.postRotate(degrees);  
          Bitmap outputBitmap = Bitmap.createBitmap(mCacheBitmap, 0, 0, mCacheBitmap.getWidth(), mCacheBitmap.getHeight(), matrix, true);  

          if (outputBitmap.getWidth() <= canvas.getWidth()) {  
              mScale = getRatio(outputBitmap.getWidth(), outputBitmap.getHeight(), canvas.getWidth(), canvas.getHeight());  
          } else {  
              mScale = getRatio(canvas.getWidth(), canvas.getHeight(), outputBitmap.getWidth(), outputBitmap.getHeight());  
          }  

          if (mScale != 0) {  
              canvas.scale(mScale, mScale, 0, 0);  
          }  
          Log.d(TAG, "mStretch value: " + mScale);  

          canvas.drawBitmap(outputBitmap, 0, 0, null);  

          if (mFpsMeter != null) {  
              mFpsMeter.measure();  
              mFpsMeter.draw(canvas, 20, 30);  
          }  
          getHolder().unlockCanvasAndPost(canvas);  

      }  
  }  
```

```java
private float getRatio(int widthSource, int heightSource, int widthTarget, int heightTarget) {  
   if (widthTarget <= heightTarget) {  
       return (float) heightTarget / (float) heightSource;  
   } else {  
       return (float) widthTarget / (float) widthSource;  
   }  
```

{% embed url="https://stackoverflow.com/questions/14816166/rotate-camera-preview-to-portrait-android-opencv-camera" %}




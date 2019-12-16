# Android Opencv Preview 방향전환 문제

CameraBridgeViewBase를 일부 수정해야한다. 

* updateMatrix\(\) 메소드 추가

```java
//I added new field
private final Matrix mMatrix = new Matrix();

//added updateMatrix method
private void updateMatrix() {
        float hw = this.getWidth() / 2.0f;
        float hh = this.getHeight() / 2.0f;
        boolean isFrontCamera = Camera.CameraInfo.CAMERA_FACING_FRONT == mCameraIndex;
        mMatrix.reset();
        if (isFrontCamera) {
            mMatrix.preScale(-1, 1, hw, hh);
        }
        mMatrix.preTranslate(hw, hh);
        if (isFrontCamera)
            mMatrix.preRotate(270);
        else
            mMatrix.preRotate(90);
        mMatrix.preTranslate(-hw, -hh);
}
```

* layout 오버라이드  updateMatrix\(\) 추가 

```java
@Override
public void layout(int l, int t, int r, int b) {
        super.layout(l, t, r, b);
        updateMatrix();
}
```

* onMeasure 오버라이드  updateMatrix\(\) 추가

```java
@Override
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
       super.onMeasure(widthMeasureSpec, heightMeasureSpec);
       updateMatrix();
}
```

*  CameraBridgeViewBase.java의 deliverAndDrawFrame 변경

```java
protected void deliverAndDrawFrame(CvCameraViewFrame frame) {
... 

    int saveCount = canvas.save(); 
    canvas.setMatrix(mMatrix); 
    mScale = Math.max((float) canvas.getHeight() / mCacheBitmap.getWidth(), (float) canvas.getWidth() / mCacheBitmap.getHeight());

...
    canvas.restoreToCount(saveCount); 
...
}
```

SampleFile : [CameraBridgeViewBase.java](https://gist.github.com/thongdoan/d73267eb58863f70c77d1288fe5cd3a4)

{% embed url="https://stackoverflow.com/questions/16669779/opencv-camera-orientation-issue" %}




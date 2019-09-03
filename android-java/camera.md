---
description: '#부스트코스'
---

# Camera

### 카메라앱 실행 후 캡쳐

```java
Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
intent.putExtra(MediaStore.EXTRA_OUTPUT, Uri.fromFile(file));

if (intent.resolveActivity(getPackageManager()) != null) {
  startActivityForResult(intent, REQUEST_IMAGE_CAPTURE);
}
```

### 카메라 미리보기 및 캡쳐

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
public class MainActivity extends AppCompatActivity {

    ImageView imgCapture;
    CameraSurfaceView sfvCapture;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        imgCapture = findViewById(R.id.img_capture);
        sfvCapture = findViewById(R.id.sfv_capture);

        Button btnCapture = findViewById(R.id.btn_capture);
        btnCapture.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                capture();
            }
        });
    }

    private void capture() {
        sfvCapture.capture(new Camera.PictureCallback() {
            @Override
            public void onPictureTaken(byte[] data, Camera camera) {
                BitmapFactory.Options options = new BitmapFactory.Options();
                options.inSampleSize = 8;
                Bitmap bitmap = BitmapFactory.decodeByteArray(data,0, data.length);

                imgCapture.setImageBitmap(bitmap);

                camera.startPreview();
            }
        });
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="CameraSufaceView.java" %}
```java
public class CameraSurfaceView extends SurfaceView implements SurfaceHolder.Callback {
    SurfaceHolder holder;
    Camera camera = null;

    public CameraSurfaceView(Context context) {
        super(context);
        init();
    }

    public CameraSurfaceView(Context context, AttributeSet attrs) {
        super(context, attrs);
        init();
    }

    private void init() {
        holder = getHolder();
        holder.addCallback(this);
    }

    //생성시 호출
    @Override
    public void surfaceCreated(SurfaceHolder holder) {
        camera = Camera.open();

        try {
            camera.setPreviewDisplay(holder);

        } catch (Exception e) {

        }
    }

    //변경시 호출
    @Override
    public void surfaceChanged(SurfaceHolder holder, int format, int width, int height) {
        camera.startPreview();

    }

    //종료시 호출
    @Override
    public void surfaceDestroyed(SurfaceHolder holder) {
        camera.stopPreview();
        camera.release();
        camera = null;
    }

    public boolean capture(Camera.PictureCallback callback){
        if(camera != null){
            camera.takePicture(null,null,callback);
            return true;
        }else{
            return false;
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}


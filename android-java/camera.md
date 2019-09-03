---
description: '#부스트코스'
---

# Camera

## 권한 부여 

Android 22 이하 인 경우 위험 권한 자동부여되지만 23이상 인경우 권한을 부여해주어야한다. 

{% code-tabs %}
{% code-tabs-item title="Manifest.xml" %}
```markup
<uses-permission android:name="android.permission.CAMERA"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
 initPermission(Manifest.permission.CAMERA, REQUEST_CODE_CAMERA);
 initPermission(Manifest.permission.READ_EXTERNAL_STORAGE, REQUEST_CODE_READ_EXTERNAL_STORAGE);
 initPermission(Manifest.permission.WRITE_EXTERNAL_STORAGE, REQUEST_CODE_WRITE_EXTERNAL_STORAGE);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
private void initPermission(String permission, int RequestCode) {
        //Manifest의 권한 확인
        int permissionCheck = ContextCompat.checkSelfPermission(this, permission);
        //권한 여부 확인
        if (permissionCheck == PackageManager.PERMISSION_GRANTED) {
            Toast.makeText(this, "권한 주어져 있음.", Toast.LENGTH_LONG).show();
        } else {
            Toast.makeText(this, "권한 없음", Toast.LENGTH_LONG).show();
            if (ActivityCompat.shouldShowRequestPermissionRationale(this, permission)) {
                Toast.makeText(this, "권한 설명 필요함", Toast.LENGTH_LONG).show();
            } else {
                //권한 요청
                ActivityCompat.requestPermissions(this, new String[]{permission}, RequestCode);
            }
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
//    super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        switch (requestCode) {
            case REQUEST_CODE_CAMERA:
                if (grantResults.length > 0) {
                    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[0] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
            case REQUEST_CODE_READ_EXTERNAL_STORAGE:
                if (grantResults.length > 0) {
                    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[0] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
            case REQUEST_CODE_WRITE_EXTERNAL_STORAGE:
                if (grantResults.length > 0) {
                    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[0] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
        }
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 카메라앱 실행 후 캡쳐

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
intent.putExtra(MediaStore.EXTRA_OUTPUT, Uri.fromFile(file));

if (intent.resolveActivity(getPackageManager()) != null) {
  startActivityForResult(intent, REQUEST_IMAGE_CAPTURE);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    if(requestCode == REQUEST_IMAGE_CAPTURE & requestCode == Activity.RESULT_OK){
            BitmapFactory.Options options = new BitmapFactory.Options();
            options.inSampleSize = 8;
            Bitmap bitmap = BitmapFactory.decodeFile(file.getAbsolutePath(),options);
            imgCapture.setImageBitmap(bitmap);
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 카메라 미리보기 및 캡쳐

### 사진 찍은 결과 보여주기  

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
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
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 미리보기를 위한 SurfaceView

#### 1\) SufaceView를 제어할 holder를 가져오고 SurfaceHolder.Callback 을 추가 

{% code-tabs %}
{% code-tabs-item title="CameraSufaceView.java" %}
```java
private void init() {
        holder = getHolder();
        holder.addCallback(this);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 2\)  SurfaceHolder.Callback의 메소 구현 

* surfaceCreated : 생성시 호출
* surfaceChanged : 변경시 호출
* surfaceDestroyed : 종료시 호출 

카메라를 열고 미리보기 설정을 한다. 

{% code-tabs %}
{% code-tabs-item title="CameraSufaceView.java" %}
```java
//생성시 호출
    @Override
    public void surfaceCreated(SurfaceHolder holder) {
        camera = Camera.open();

        try {
            camera.setPreviewDisplay(holder);

        } catch (Exception e) {

        }
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

미리보기를 시작한다. 

{% code-tabs %}
{% code-tabs-item title="CameraSufaceView.java" %}
```java
//변경시 호출
    @Override
    public void surfaceChanged(SurfaceHolder holder, int format, int width, int height) {
        camera.startPreview();

    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

종료시 미리보기를 종료하고 할당한 메모리를 해제한다. 

{% code-tabs %}
{% code-tabs-item title="CameraSufaceView.java" %}
```java
//종료시 호출
    @Override
    public void surfaceDestroyed(SurfaceHolder holder) {
        camera.stopPreview();
        camera.release();
        camera = null;
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 전체 소스코드 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
public class MainActivity extends AppCompatActivity {

    private static final int REQUEST_CODE_CAMERA = 1;
    private static final int REQUEST_CODE_READ_EXTERNAL_STORAGE = 2;
    private static final int REQUEST_CODE_WRITE_EXTERNAL_STORAGE = 3;


    ImageView imgCapture;
    CameraSurfaceView sfvCapture;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initPermission(Manifest.permission.CAMERA, REQUEST_CODE_CAMERA);
        initPermission(Manifest.permission.READ_EXTERNAL_STORAGE, REQUEST_CODE_READ_EXTERNAL_STORAGE);
        initPermission(Manifest.permission.WRITE_EXTERNAL_STORAGE, REQUEST_CODE_WRITE_EXTERNAL_STORAGE);

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
                Bitmap bitmap = BitmapFactory.decodeByteArray(data, 0, data.length);

                imgCapture.setImageBitmap(bitmap);

                camera.startPreview();
            }
        });
    }

    private void initPermission(String permission, int RequestCode) {
        //Manifest의 권한 확인
        int permissionCheck = ContextCompat.checkSelfPermission(this, permission);
        //권한 여부 확인
        if (permissionCheck == PackageManager.PERMISSION_GRANTED) {
            Toast.makeText(this, "권한 주어져 있음.", Toast.LENGTH_LONG).show();
        } else {
            Toast.makeText(this, "권한 없음", Toast.LENGTH_LONG).show();
            if (ActivityCompat.shouldShowRequestPermissionRationale(this, permission)) {
                Toast.makeText(this, "권한 설명 필요함", Toast.LENGTH_LONG).show();
            } else {
                //권한 요청
                ActivityCompat.requestPermissions(this, new String[]{permission}, RequestCode);
            }
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
//    super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        switch (requestCode) {
            case REQUEST_CODE_CAMERA:
                if (grantResults.length > 0) {
                    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[0] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
            case REQUEST_CODE_READ_EXTERNAL_STORAGE:
                if (grantResults.length > 0) {
                    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[0] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
            case REQUEST_CODE_WRITE_EXTERNAL_STORAGE:
                if (grantResults.length > 0) {
                    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[0] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
        }
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

{% embed url="https://developer.android.com/guide/topics/media/camera.html" %}

{% embed url="https://developer.android.com/training/camera/cameradirect.html" %}

{% embed url="https://developer.android.com/training/camera/photobasics.html" %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17103/" %}


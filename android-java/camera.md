---
description: '#부스트코스'
---

# Camera



```java
Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
intent.putExtra(MediaStore.EXTRA_OUTPUT, Uri.fromFile(file));

if (intent.resolveActivity(getPackageManager()) != null) {
  startActivityForResult(intent, REQUEST_IMAGE_CAPTURE);
}
```



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


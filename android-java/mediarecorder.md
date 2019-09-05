---
description: '#부스트코스'
---

# MediaRecorder

### AudioRecord 시작 

* setAudioSource : 녹음 입력 방
* setOutputFormat : 저장 포맷 
* setAudioEncoder : encoding 방식 
* setOutputFile : 녹음을 저장할 파일 경로 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
private void startRecordAudio() {
        recorder = new MediaRecorder();
        recorder.setAudioSource(MediaRecorder.AudioSource.MIC);
        recorder.setOutputFormat(MediaRecorder.OutputFormat.MPEG_4);
        recorder.setAudioEncoder(MediaRecorder.AudioEncoder.DEFAULT);
        recorder.setOutputFile(filename);

        try {
            recorder.prepare();
            recorder.start();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### AudioRecord 정지 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
private void stopRecordAudio() {
        if (recorder != null) {
            recorder.stop();
            recorder.release();
            recorder = null;
            Toast.makeText(this, "녹음정지", Toast.LENGTH_LONG).show();
        }
    }    
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### MediaPlayer 관련 메소드  

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
    private void stopMusic() {

        if (mediaPlayer != null && mediaPlayer.isPlaying()) {
            mediaPlayer.stop();
        }
        Toast.makeText(this, "정지", Toast.LENGTH_LONG).show();
    }

    private void resumeMusic() {
        if (mediaPlayer != null && mediaPlayer.isPlaying()) {
            mediaPlayer.seekTo(position);
            mediaPlayer.start();
        }
        Toast.makeText(this, "재개", Toast.LENGTH_LONG).show();

    }

    private void pauseMusic() {
        if (mediaPlayer != null) {
            position = mediaPlayer.getCurrentPosition();
            mediaPlayer.pause();
        }
        Toast.makeText(this, "일시정지", Toast.LENGTH_LONG).show();

    }

    private void playRecordFile() {
        try {
            closePlayer();
            mediaPlayer = new MediaPlayer();
            mediaPlayer.setDataSource(filename);
            mediaPlayer.prepare();
            mediaPlayer.start();

        } catch (IOException e) {
            e.printStackTrace();
        }

        Toast.makeText(this, "재생", Toast.LENGTH_LONG).show();
    }

    public void closePlayer() {
        if (mediaPlayer != null) {
            mediaPlayer.release();
            mediaPlayer = null;
        }
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 권한 부여 

{% code-tabs %}
{% code-tabs-item title="AndroidManifest.xml" %}
```markup
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>roid
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="MainActivitiy.java" %}
```java
String[] permissions = {
        Manifest.permission.READ_EXTERNAL_STORAGE,
        Manifest.permission.WRITE_EXTERNAL_STORAGE,
        Manifest.permission.RECORD_AUDIO,
};
initPermission(permissions,REQUEST_CODE_READ_EXTERNAL_STORAGE);
initPermission(permissions,REQUEST_CODE_WRITE_EXTERNAL_STORAGE);
initPermission(permissions,REQUEST_CODE_RECORD_AUDIO);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
private void initPermission(String[] permissions, int requestCode) {
            //Manifest의 권한 확인
            int permissionCheck = ContextCompat.checkSelfPermission(this, permissions[requestCode-1] );
            //권한 여부 확인
            if (permissionCheck == PackageManager.PERMISSION_GRANTED) {
                Toast.makeText(this, "권한 주어져 있음.", Toast.LENGTH_LONG).show();
            } else {
                Toast.makeText(this, "권한 없음", Toast.LENGTH_LONG).show();
                if (ActivityCompat.shouldShowRequestPermissionRationale(this, permissions[requestCode-1])) {
                    Toast.makeText(this, "권한 설명 필요함", Toast.LENGTH_LONG).show();
                } else {
                    //권한 요청
                    ActivityCompat.requestPermissions(this, permissions, requestCode);
                }
            }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
//        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        switch (requestCode) {
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
                break;
            case REQUEST_CODE_WRITE_EXTERNAL_STORAGE:
                if (grantResults.length > 0) {
                    if (grantResults[1] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[1] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
                break;
            case REQUEST_CODE_RECORD_AUDIO:
                if (grantResults.length > 0) {
                    if (grantResults[2] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[2] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
                break;

        }
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17106/" %}




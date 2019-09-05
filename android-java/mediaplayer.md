---
description: '#부스트코스'
---

# Mediaplayer

## 음악 재생

### 인터넷 음악 재생 

```java
private void playUriMusic() {
    String url = "https://www.all-birds.com/Sound/western%20bluebird.wav";
    mediaPlayer = new MediaPlayer();
    try {
        mediaPlayer.reset();
        mediaPlayer.setDataSource(url);
        mediaPlayer.prepare();
        mediaPlayer.start();

    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

### 권한 부여 

```markup
<uses-permission android:name="android.permission.INTERNET"/>
```

### 프로젝트 음악 재생 

```java
private void playProjectMusic() {
        try {
            AssetFileDescriptor afd = getAssets().openFd("melodyloops-skater.mp3");
            mediaPlayer = new MediaPlayer();
            mediaPlayer.setDataSource(afd.getFileDescriptor(), afd.getStartOffset(), afd.getLength());
            mediaPlayer.prepare();
            mediaPlayer.start();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

### SD 카드 음악 재생 

```java
private void playSdcardMusic(){
    try {
        String filepath = "/sdcard/a.mp3";
        MediaPlayer mediaPlayer = new MediaPlayer();
        mediaPlayer.setDataSource(filepath);
        mediaPlayer.prepare();
        mediaPlayer.start();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

### 일시정지

```java
private void pauseMusic() {
    if(mediaPlayer != null){
        position = mediaPlayer.getCurrentPosition();
        mediaPlayer.pause();
    }
    Toast.makeText(this,"일시정지",Toast.LENGTH_LONG).show();
}
```

### 다시 시작

```java
private void resumeMusic() {
    if(mediaPlayer != null && mediaPlayer.isPlaying()){
        mediaPlayer.seekTo(position);
        mediaPlayer.start();
    }
    Toast.makeText(this,"재개",Toast.LENGTH_LONG).show();
}
```

### 정지 

```java
private void stopMusic() {
    if(mediaPlayer != null && mediaPlayer.isPlaying()){
        mediaPlayer.stop();
    }
    Toast.makeText(this,"정지",Toast.LENGTH_LONG).show();
}
```

### MediaPlayer 해제 

```java
public void closePlayer() {
    if (mediaPlayer != null){
        mediaPlayer.release();
        mediaPlayer = null;
    }
}
```

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17104/" %}




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

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17104/" %}




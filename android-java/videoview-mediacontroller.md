---
description: '#부스트코스'
---

# VideoView, MediaController

## 동영상 재생 

### 1\) layout

#### VideoView 를 사용한다. 

{% code-tabs %}
{% code-tabs-item title="activity\_main.xml" %}
```markup
<VideoView
    android:id="@+id/videoView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 2\) 동영상 load

* setMediaController : MediaController를 객체를 VideoView에 설정
* setVideoURI : 파일위치 지정
* requestFocus : 재생버튼 뷰를 요청한다.  

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
private void playVideo() {
    VideoView videoView = (VideoView) findViewById(R.id.videoView);
    String VIDEO_URL = "http://sites.google.com/site/ubiaccessmobile/sample_video.mp4";
    MediaController mc = new MediaController(this);
    videoView.setMediaController(mc);
    videoView.setVideoURI(Uri.parse(VIDEO_URL));
    videoView.requestFocus();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 3\) 동영상 재생 

```java
Button btnPlay = findViewById(R.id.btn_play);
btnPlay.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        videoView.start();
    }
});
```

{% hint style="info" %}
**VideoView 메소드** 

seekTo\(int msec\) : 재생 위치 설정

start\(\) : 재생 시 

pause\(\) : 일시정지 시

resume\(\) : 다시 재생 시 
{% endhint %}

![](../.gitbook/assets/videoview.gif)


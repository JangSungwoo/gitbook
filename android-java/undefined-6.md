---
description: '#부스트코스'
---

# Activity LifeCycle

다음 사진은 공식 문서의 Activity LifeCycle을 나타내는 사진이다. 

![Activity LifeCly](../.gitbook/assets/activity_lifecycle.png)

### 액티비티가 실행될 때 

`onCreate()` -&gt; `onStart()` -&gt; `onResume()`

### 액티비티가 종료될 때 

`onPause()` -&gt; `onStop()` -&gt; `onDestory()` 

### 액티비티가 일시정지될 때 

`onPause()` -&gt; `onStop()`

### 일시정지 된 액티비티가 다시 활성화 되었을 때 

`onRestart()` -&gt; `onStart()` -&gt; `onResume()`

{% embed url="https://developer.android.com/guide/components/activities/activity-lifecycle" %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17067/" %}




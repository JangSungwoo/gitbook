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

## 데이터의 복구 

수명주기 메소드가 자동호출되도록 만든 이유는 데이터나 상태정보를 복구하기 위해서 만들어 진 것이다. 

sharedPreference 를 사용하여 애플리케이션이 종료될때\(`onPause()`\) 데이터나 상태정보를 임시저장하고 다시 실행될 때\(onResume\(\)\) 가져와서 사용할 수 있다.

```java
@Override
protected void onPause() {
    super.onPause();
    Toast.makeText(this,"onPause() 호출됨",Toast.LENGTH_LONG).show();

    SharedPreferences pref = getSharedPreferences("pref", Activity.MODE_PRIVATE);
    SharedPreferences.Editor editor = pref.edit();
    editor.putString("name", "안드로이드");
    editor.commit();
}
@Override
protected void onResume() {
    super.onResume();
    Toast.makeText(this,"onResume() 호출됨",Toast.LENGTH_LONG).show();
    SharedPreferences pref = getSharedPreferences("pref",Activity.MODE_PRIVATE);
    if(pref !=null){
        String name = pref.getString("name","");
        Toast.makeText(this,"복구된 이름 : "+ name,Toast.LENGTH_LONG).show();
    }
}

```

{% embed url="https://developer.android.com/guide/components/activities/activity-lifecycle" %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17067/" %}




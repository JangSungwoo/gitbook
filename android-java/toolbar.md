# Toolbar 버튼

drawer인경우 res &gt; menu 에서 설정을 한다. 

다음은 setting 버튼의 예시이다. 

{% code title="movie\_app\_drawer.xml" %}
```markup
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/action_settings"
        android:orderInCategory="100"
        android:title="@string/action_settings"
        app:showAsAction="never" />
</menu>
```
{% endcode %}



```java
  @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        //Toolbar 버튼
        getMenuInflater().inflate(R.menu.movie_app_drawer, menu);
        return true;
    }
```



```java
getMenuInflater().inflate(R.menu.movie_app_drawer, menu);
```

이 코드는 menu에 정의된 버튼을 inflate 하는 단계로써 추가 및 제거가 가능하다. 


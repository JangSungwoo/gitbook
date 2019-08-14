---
description: '#부스트코스'
---

# ActionBar

액션바 구성하기 

### 안드로이드의 메뉴 

* 옵션메뉴 
* 컨텍스트 메뉴 

1\) res 아래에 menu 폴더 생성 후 menu\_main.xml 을 추가한다.

2\) menu\_main.xml 에서 원하는 menu를 추가한다. 

{% code-tabs %}
{% code-tabs-item title="menu\_main.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menu_refresh"
        android:icon="@drawable/menu_refresh"
        android:title="새로고침"
        app:showAsAction="always" />

    <item
        android:id="@+id/menu_search"
        android:icon="@drawable/menu_search"
        android:title="검색"
        app:showAsAction="always" />

    <item
        android:id="@+id/menu_settings"
        android:icon="@drawable/menu_settings"
        android:title="설정"
        app:showAsAction="always" />
</menu>

```
{% endcode-tabs-item %}
{% endcode-tabs %}

  3\) MainActivity 에서 `onCreateOptionsMenu` 를 재 정의 한다. 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main,menu);
    return true;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

4\) 각 메뉴의 클릭 이벤트를 확인하기 위해서는 `onOptionsItemSelected` 를 재정의 한다. 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    int curId = item.getItemId();
    switch (curId){
        case R.id.menu_refresh:
            Toast.makeText(this,"새로고침 메뉴 클릭됨",Toast.LENGTH_LONG).show();
            break;
        case R.id.menu_search:
            Toast.makeText(this,"검색 메뉴 클릭됨",Toast.LENGTH_LONG).show();
            break;
        case R.id.menu_settings:
            Toast.makeText(this,"설정 메뉴 클릭됨",Toast.LENGTH_LONG).show();
            break;
         default:
             break;
    }
    return super.onOptionsItemSelected(item);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
초기에 ActionBar 에 대한 설정은 res &gt; values &gt; style.xml 에 정의 되어있다. 

{% code-tabs %}
{% code-tabs-item title="style.xml" %}
```markup
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

</resources>
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endhint %}


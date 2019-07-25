---
description: '#부스트코스'
---

# ListView

## 1\) 아이템을 위한 XML 레이아웃을 정의

{% code-tabs %}
{% code-tabs-item title="item\_view.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="horizontal">

    <de.hdodenhof.circleimageview.CircleImageView
        android:layout_width="40dp"
        android:layout_height="40dp"
        android:layout_margin="10dp"
        android:src="@drawable/user1"
        app:civ_border_width="2dp"
        app:civ_border_color="#FFCCCCCC"/>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="kym71***"
            android:textSize="10dp"
            android:textStyle="bold"
            android:textColor="#000000"/>
    </LinearLayout>
</LinearLayout>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* de.hdodenhof.circleimageview.CircleImageView

  * Circle 모양의 이미지뷰를 나타내기 위한 태그
  * src/build.gradle 파일의 dependencies에 추가



  {% code-tabs %}
  {% code-tabs-item title="build.gradle" %}
  ```text
  dependencies {
      implementation fileTree(dir: 'libs', include: ['*.jar'])
      implementation 'com.android.support:appcompat-v7:28.0.0'
      implementation 'com.android.support.constraint:constraint-layout:1.1.3'
      testImplementation 'junit:junit:4.12'
      androidTestImplementation 'com.android.support.test:runner:1.0.2'
      androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'

      implementation 'de.hdodenhof:circleimageview:2.2.0'

  }
  ```
  {% endcode-tabs-item %}
  {% endcode-tabs %}

## 

## 2\) 아이템을 위한 뷰 정의

## 3\) 어댑터 정의

## 4\) 리스트뷰 정의




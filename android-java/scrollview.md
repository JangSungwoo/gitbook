---
description: '#부스트코스'
---

# Scrollview

스크롤 뷰는 상하, 좌우 모두 스크롤이 가능하다.

* 상하 스크롤 : ScrollView
* 좌우 스크롤 : HorizontalScrollView

#### 상하 스크롤 

```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Hello\nHello\nHello\nHello\nHello\nHello\nHello\n"
                android:textSize="70dp" />
        </LinearLayout>

    </ScrollView>

</LinearLayout>
```

#### 상하좌우스크롤

```markup
<HorizontalScrollView
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/android_robot" />
    </ScrollView>

</HorizontalScrollView>
```

{% embed url="https://www.edwith.org/boostcourse-android/lecture/20484/" %}




---
description: '#부스트코스'
---

# Tab

1\) design 패키지 참조  

File &gt; Project Structure &gt; Dependencies &gt; + Library Dependency &gt; com.android.support:design 추가 

2\) activity\_main.xml 파일을 수정한다. 

{% code-tabs %}
{% code-tabs-item title="activity\_main.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <android.support.design.widget.CoordinatorLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <android.support.design.widget.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar">

            <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="@color/colorPrimaryDark"
                android:elevation="1dp"
                android:theme="@style/ThemeOverlay.AppCompat.Dark">

            </android.support.v7.widget.Toolbar>

            <TableLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="@android:color/background_light"
                android:elevation="1dp"
                android:tabGravity="fill"
                android:tabMode="fixed"
                android:tabSelectedTextColor="@color/colorAccent"
                android:tabTextColor="@color/colorPrimaryDark">

            </TableLayout>
        </android.support.design.widget.AppBarLayout>

        <FrameLayout
            android:id="@+id/container"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

        </FrameLayout>
    </android.support.design.widget.CoordinatorLayout>

</RelativeLayout>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

3\) 탭에서 사용할 fragment 파일을 생성한다.

{% code-tabs %}
{% code-tabs-item title="Firstfragment.java" %}
```java
public class FirstFragment extends Fragment {
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        ViewGroup rootView = (ViewGroup) inflater.inflate(R.layout.fragment_first,container,false);
        return rootView;
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="fragment\_first.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="@android:color/holo_blue_dark">

    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="첫번째 화면"
        android:textSize="40dp" />

    <Button
        android:id="@+id/btn_next"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="다음"/>
</LinearLayout>
```
{% endcode-tabs-item %}
{% endcode-tabs %}


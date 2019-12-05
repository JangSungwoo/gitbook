---
description: '#부스트코스'
---

# Navigation Drawer

**1\) 내용을 넣고 싶은 위치에 FrameLayout 을 추가한다.** 

{% code title="activity\_main.xml" %}
```markup
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:openDrawer="start">

    <android.support.design.widget.CoordinatorLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <android.support.design.widget.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:theme="@style/AppTheme.AppBarOverlay">

            <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                android:background="?attr/colorPrimary"
                app:popupTheme="@style/AppTheme.PopupOverlay" />

        </android.support.design.widget.AppBarLayout>

        <FrameLayout
            android:id="@+id/container"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:layout_behavior="android.support.design.widget.AppBarLayout$ScrollingViewBehavior">

        </FrameLayout>
    </android.support.design.widget.CoordinatorLayout>

    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:fitsSystemWindows="true"
        app:headerLayout="@layout/nav_header_main"
        app:menu="@menu/activity_main_drawer" />

</android.support.v4.widget.DrawerLayout>

```
{% endcode %}

**2\) fragment 설정** 

{% tabs %}
{% tab title="fragment\_first.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/holo_blue_dark">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="첫번째 프래그먼트"
        android:textSize="40dp" />

</FrameLayout>
```
{% endtab %}

{% tab title="FirstFragment.java" %}
```java
public class firstFragment extends Fragment {

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        ViewGroup rootView = (ViewGroup) inflater.inflate(R.layout.fragment_first,container,false);
        return rootView;
    }
}
```
{% endtab %}
{% endtabs %}

**3\) Navigation Drawer의 head 및 view의 아이템을 설정** 

기본값인경우 **프로필사진변경, 이름, 메일** 항목은 layout &gt; nav\_head\_main.xml 파일에서 수정한다. 

{% code title="nav\_head\_main.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="@dimen/nav_header_height"
    android:background="@drawable/side_nav_bar"
    android:gravity="bottom"
    android:orientation="vertical"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:theme="@style/ThemeOverlay.AppCompat.Dark">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="70dp"
        android:layout_height="70dp"
        android:contentDescription="@string/nav_header_desc"
        android:paddingTop="@dimen/nav_header_vertical_spacing"
        app:srcCompat="@drawable/jang" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:paddingTop="@dimen/nav_header_vertical_spacing"
        android:text="@string/nav_header_title"
        android:textAppearance="@style/TextAppearance.AppCompat.Body1" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/nav_header_subtitle" />

</LinearLayout>
```
{% endcode %}

Navigation view를 설정하기 위해서는 menu &gt; activity\_main\_drawer.xml에서 변경이 가능하다.  

{% code title="activity\_main\_drawer.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    tools:showIn="navigation_view">

    <group android:checkableBehavior="single">
        <item
            android:id="@+id/nav_first"
            android:icon="@drawable/ic_menu_camera"
            android:title="첫번재화면" />
        <item
            android:id="@+id/nav_second"
            android:icon="@drawable/ic_menu_gallery"
            android:title="두번째화면" />
        <item
            android:id="@+id/nav_third"
            android:icon="@drawable/ic_menu_slideshow"
            android:title="세번째화면" />

    </group>

</menu>
```
{% endcode %}

onNavigationItemSelected에서 item.getItemId\(\) 를 통해 선택된 아이템을 비교하여 클릭이벤트를 제어할 수 있다. 

onFragmentSelected는 선택된 아이템에 해당하는 fragment를 FragmentManager를 통해 infalte 한다. 

{% code title="MainActivity.java" %}
```java
@SuppressWarnings("StatementWithEmptyBody")
@Override
public boolean onNavigationItemSelected(MenuItem item) {
    // Handle navigation view item clicks here.
    int id = item.getItemId();

    if (id == R.id.nav_first) {
        Toast.makeText(this,"첫번째 메뉴 화면",Toast.LENGTH_LONG).show();
        onFragmentSelected(0,null);
    } else if (id == R.id.nav_second) {
        Toast.makeText(this,"두번째 메뉴 화면",Toast.LENGTH_LONG).show();
        onFragmentSelected(1,null);
    } else if (id == R.id.nav_third) {
        Toast.makeText(this,"세번째 메뉴 화면",Toast.LENGTH_LONG).show();
        onFragmentSelected(2,null);
    }

    DrawerLayout drawer = findViewById(R.id.drawer_layout);
    drawer.closeDrawer(GravityCompat.START);
    return true;
}
 @Override
    public void onFragmentSelected(int position, Bundle bundle) {
        Fragment curFragment = null;

        if(position == 0){
            curFragment = firstFragment;
            toolbar.setTitle("첫번째화면");
        }else if(position == 1){
            curFragment = secondFragment;
            toolbar.setTitle("두번째화면");
        }else if(position == 2){
            curFragment = thirdFragment;
            toolbar.setTitle("세번째화면");
        }

        getSupportFragmentManager().beginTransaction().replace(R.id.container,curFragment).commit();
    }
```
{% endcode %}





![](../.gitbook/assets/navigation_drawer.gif)





{% embed url="https://www.edwith.org/boostcourse-android/lecture/20684/" %}




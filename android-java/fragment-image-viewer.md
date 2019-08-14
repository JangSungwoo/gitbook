---
description: '#부스트코스'
---

# Fragment Image Viewer

## 프래그먼트로 이미지뷰어 만들기 

버튼을 클릭하여 이미지를 변경하는 예제를 해보자. 

1\) 버튼리스트를 Fragment로 정의 한다. \( fragment\_list.xml \)

2\) 이미지뷰어를 Fragment로 정의한다. \( fragment\_viewer.xml \) 

3\) ListFragment에서 ViewGroup과 fragment\_list를 inflate한다. 

4\) ViewerFragment에서 ViewGroup과 fragment\_viewer를 inflate 한다. 

5\) ListFragment에서 onAttach를 재 정의하고 activity를 가져온다.

6\) ListFragment에서 각 버튼 클릭시 MainActivity의 onImageChange를 호출한다. 

7\) MainActivity의 onImageChange는 ViewerFragment를 호출한다. 

8\) activity\_main.xml에 ListFragment, ViewerFragment를 추가한다. 

9\) MainActivity에 FragmentManager를 사용하여 ListFragment, ViewFragment를 정의한다. 

10\) View의 setImage를 호출하여 이미지를 설정한다. 



{% code-tabs %}
{% code-tabs-item title="activity\_main.xml" %}
```text
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <fragment
        android:id="@+id/listFragment"
        android:name="com.example.examfragmentimageviewer.ListFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />

    <fragment
        android:id="@+id/viewerFragment"
        android:name="com.example.examfragmentimageviewer.ViewerFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />
</LinearLayout>
```
{% endcode-tabs-item %}
{% endcode-tabs %}














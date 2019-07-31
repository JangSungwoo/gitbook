---
description: '#부스트코스'
---

# TableLayout

TableLayout은 TableRow를 사용하여 view를 배치할 수 있다.

LinearLayout과의 차이점은 orientation설정 없이 horizontal 방식으로 편리하게 배치할 수 있다는 점이다.

 TableLayout의에 stretchColumns 속성을 사용하여 view의 비중을 제어할 수 있다.

또한 Talayout의 layout\_column 속성을 통해 순서도 지정할 수 있다.

{% tabs %}
{% tab title=" Basic" %}
![](../.gitbook/assets/image%20%285%29.png)

```markup
<?xml version="1.0" encoding="utf-8"?>
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <Button
            android:id="@+id/btnTableRowLeft"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="LeftButton"/>
        <Button
            android:id="@+id/btnTableRowCenter"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="CenterButton"/>
        <Button
            android:id="@+id/btnTableRowRight"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="RightButton"/>
    </TableRow>

</TableLayout>
```
{% endtab %}

{% tab title="stretchColumns" %}
![](../.gitbook/assets/image%20%286%29.png)

```markup
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:stretchColumns="0,1,2"
    >

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <Button
            android:id="@+id/btnTableRowLeft"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="LeftButton"/>
        <Button
            android:id="@+id/btnTableRowCenter"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="CenterButton"/>
        <Button
            android:id="@+id/btnTableRowRight"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="RightButton"/>
    </TableRow>
    
</TableLayout>
```
{% endtab %}

{% tab title="layout\_column" %}
![](../.gitbook/assets/image%20%289%29.png)

```markup
<TableRow
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <Button
            android:id="@+id/btnTableRowOk"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_column="1"
            android:text="OK"/>
        <Button
            android:id="@+id/btnTableRowCancel"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_column="2"
            android:text="Cancel"/>
    </TableRow>

```
{% endtab %}
{% endtabs %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17050/" %}




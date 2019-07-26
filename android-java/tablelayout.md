---
description: '#부스트코스'
---

# TableLayout

{% tabs %}
{% tab title=" Basic" %}
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
![](../.gitbook/assets/image%20%288%29.png)

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




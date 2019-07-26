---
description: '#부스트코스'
---

# ListView

## 1\) 아이템을 위한 XML 레이아웃을 정의

{% code-tabs %}
{% code-tabs-item title="singer\_item.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">

    <ImageView
        android:layout_width="80dp"
        android:layout_height="80dp"
        android:src="@mipmap/ic_launcher" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginLeft="10dp"
        android:orientation="vertical">

        <TextView
            android:id="@+id/tvName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="이름"
            android:textColor="@color/colorPrimaryDark"
            android:textSize="30dp" />

        <TextView
            android:id="@+id/tvMobile"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="전화번호"
            android:layout_marginTop="8dp"
            android:textColor="@color/colorPrimaryDark"
            android:textSize="24dp" />
    </LinearLayout>
</LinearLayout>
```
{% endcode-tabs-item %}
{% endcode-tabs %}



## 2\) 아이템을 위한 뷰 정의

```java
public class SingerItemView extends LinearLayout {

    TextView tvName;
    TextView tvMobile;

    public SingerItemView(Context context) {
        super(context);
        init(context);
    }

    public SingerItemView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        init(context);
    }

    private  void init(Context context){
        LayoutInflater inflater = (LayoutInflater)context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        inflater.inflate(R.layout.singer_item,this,true);

        tvName = (TextView) findViewById(R.id.tvName);
        tvMobile = (TextView) findViewById(R.id.tvMobile);

    }
    public void setTvName(String name){
        tvName.setText(name);
    }

    public void setTvMobile(String mobile){
        tvMobile.setText(mobile);
    }
}
```



## 3\) 어댑터 정의

{% code-tabs %}
{% code-tabs-item title="SingerAdapter.java" %}
```java
 cl
ass SingerAdapter extends BaseAdapter{
        ArrayList<SingerItem> items = new ArrayList<SingerItem>();

        @Override
        public int getCount() {
            return items.size();
        }

        public void addItem(SingerItem item){
            items.add(item);
        }
        @Override
        public Object getItem(int position) {
            return items.get(position);
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            SingerItemView view = new SingerItemView(getApplicationContext());
            SingerItem item = items.get(position);
            view.setTvName(item.getName());
            view.setTvMobile(item.getMobile());
            return view;
        }
    }
```
{% endcode-tabs-item %}

{% code-tabs-item title="SingerItem" %}
```java
public class SingerItem {
    String name;
    String mobile;

    public SingerItem(String name, String mobile){
        this.name = name;
        this.mobile = mobile;
    }
    public String getName(){
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setMobile(String mobile) {
        this.mobile = mobile;
    }

    @Override
    public String toString() {
        return "SingerItem{" +
                "name='" + name + '\'' +
                ", mobile='" + mobile + '\'' +
                '}';
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}



## 4\) 리스트뷰 정의






---
description: '#부스트코스'
---

# ListView



![](../.gitbook/assets/listview.png)

리스트뷰를 구현하기 위한 과정을 간략하게 그림으로 표현을 해보았다. 

간단히 설명을 하자면

1. 리스트뷰는 각 아이템을 개별적으로 표현을 하기위해서는 Adapter를 사용해야한다.
2. Adapter 내에서는 getview 메소드를 통해 각 아이템의 값들을 설정해줄 수 있다.
3. getview 메소드에서는 아이템을 위한 뷰\(ItemView\)를 통해 Item과 레이아웃 계층뷰를 만든다.\(inflation\)  
4. 5. 
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
 class SingerAdapter extends BaseAdapter{
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

리스트뷰를 선언하고 어댑터를 연결하여 리스트뷰의 아이템을 표현할 수 있다.

또한 리스트뷰의 각 아이템의 클릭이벤트 및 아이템 추가 및 제거도 가능하다. 

다음 예제는 아이템 클릭시 이름값을 토스트 메세지로 띄우고 아이템을 추가하는 소스코드이다.

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
    ListView listView = findViewById(R.id.listView);

    adapter = new SingerAdapter();
    adapter.addItem(new SingerItem("장범준","010-1234-1234",R.drawable.jang));
    adapter.addItem(new SingerItem("이적","010-1234-1234",R.drawable.lee));
    adapter.addItem(new SingerItem("아이유","010-1234-1234",R.drawable.iu));
    listView.setAdapter(adapter);

    listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
        @Override
        public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
            SingerItem item = (SingerItem) adapter.getItem(position);
            Toast.makeText(getApplicationContext(),item.name,Toast.LENGTH_LONG).show();
        }
    });

    btnAddItem = (Button) findViewById(R.id.btnAddItem);
    etName = (EditText)findViewById(R.id.etName);
    etMobile = (EditText)findViewById(R.id.etMobile);

    btnAddItem.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            String name = etName.getText().toString();
            String mobile = etMobile.getText().toString();

            adapter.addItem(new SingerItem(name,mobile,R.drawable.jang));
            //갱신
            adapter.notifyDataSetChanged();
 
       }
    });
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
아이템을 추가한 후 adapter.notifyDataSetChanged\(\); 를 사용해야만 리스트뷰가 갱신이 된다.
{% endhint %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17057/" %}









Icons made by [Freepik](https://www.flaticon.com/authors/freepik) from [www.flaticon.com](https://www.flaticon.com/) is licensed by [CC 3.0 BY](http://creativecommons.org/licenses/by/3.0/)






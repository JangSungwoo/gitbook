---
description: '#부스트코스'
---

# GridView

그리드뷰는 리스트뷰와 동일한 방식으로 구현을 하면된다.

다음 리스트뷰의 설명을 참고하자. 

{% page-ref page="listview.md" %}

단, 리스트 뷰와 그리드 뷰의 다른점은 numColumns 속성의 유무이다. 

numColumns는 열의 수를 지정하는것이다.

{% tabs %}
{% tab title="MainActivity.java" %}
```java
public class MainActivity extends AppCompatActivity {

    FoodAdapter adapter;
    EditText etName;
    EditText etPrice;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        GridView gridView = (GridView)findViewById(R.id.gridView1);

        adapter = new FoodAdapter();
        adapter.addItem(new FoodItem("샌드위치","1200원",R.drawable.sandwich));
        adapter.addItem(new FoodItem("피자","1500원",R.drawable.pizza));
        adapter.addItem(new FoodItem("치킨","8000원",R.drawable.chicken));
        adapter.addItem(new FoodItem("사이다","1000원",R.drawable.sprite));
        adapter.addItem(new FoodItem("수박","1000원",R.drawable.watermelon));
        gridView.setAdapter(adapter);

        gridView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                FoodItem item = (FoodItem) adapter.getItem(position);
                Toast.makeText(getApplicationContext(),item.name,Toast.LENGTH_LONG).show();
            }
        });

        Button btnAddItem = (Button) findViewById(R.id.btnAddItem);
        etName = (EditText) findViewById(R.id.etName);
        etPrice = (EditText) findViewById(R.id.etPrice);

        btnAddItem.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String name = etName.getText().toString();
                String mobile = etPrice.getText().toString();

                adapter.addItem(new FoodItem(name,mobile,R.drawable.food));
                //갱신
                adapter.notifyDataSetChanged();
            }
        });
    }

   
}
```
{% endtab %}

{% tab title="FoodAdapter.java" %}
```java
 class FoodAdapter extends BaseAdapter {
        ArrayList<FoodItem> items = new ArrayList<FoodItem>();

        @Override
        public int getCount() {
            return items.size();
        }

        public void addItem(FoodItem item){
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
            FoodItemView view = null;
            if(convertView == null){
                view = new FoodItemView(getApplicationContext());
            }else{
                view = (FoodItemView) convertView;
            }
            FoodItem item = items.get(position);
            view.setTvName(item.getName());
            view.setTvMobile(item.getMobile());
            view.setImgPhoto(item.photoResId);
            return view;
        }
    }
```
{% endtab %}

{% tab title="food\_item.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">

    <ImageView
        android:id="@+id/imgPhoto"
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
{% endtab %}

{% tab title="activity\_main.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnAddItem"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Add"/>

        <EditText
            android:id="@+id/etName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"/>

        <EditText
            android:id="@+id/etPrice"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"/>
    </LinearLayout>

    <GridView
        android:id="@+id/gridView1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:numColumns="2">

    </GridView>

</LinearLayout>
```
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/gridview.gif)

Icons made by [Smashicons](https://www.flaticon.com/authors/smashicons) from [www.flaticon.com](https://www.flaticon.com/) is licensed by [CC 3.0 BY](http://creativecommons.org/licenses/by/3.0/)

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17059/" %}




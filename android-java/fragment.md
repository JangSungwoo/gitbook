---
description: '#부스트코스'
---

# Fragment

## 프래그먼트\(Fragment\)란? 

하나의 액티비티 안에 여러개의 부분화면을 만들기 위해 사용하는 방법 

![](../.gitbook/assets/frament_ex1.png)

### 특징

* 여러 개의 프래그먼트를 하나의 액티비티에 조합 가능
* 자체 수명주기 \(액티비티 내에 포함되어 있어야 하며 해당 프래그먼트의 수명주기는 호스트 액티비티의 수명주기에 직접적으로 영향을 받음 \)
* 자체 입력이벤트 
* 액티비티 실행 중에 추가 및 제거가 가능한 액티비티의 모듈식 섹션
* \(예시\) 액티비티 일시정지 -&gt; 프래그먼트 일시정지, 액티비티 소멸 -&gt; 모든 프래그먼트 소멸 
* 프래그먼트 트랜잭션을 수행할 때에 액티비티가 관리하는 백 스택에도 추가 가능 
* 그러므로 Back버튼으로 프래그먼트 트랜잭션을 거꾸로 돌릴 수 있음 
* 액티비티의 일부로 추가하는 경우, 액티비티의 뷰 계층 내부의 ViewGroup안에 존재하며 해당 프래그먼트가 자신의 뷰레이아웃을 정의 
* 액티비티 레이아웃에서 &lt;fragment&gt;를 사용하거나 기존 ViewGroup에 추가\(java\) 
* UI가 없는 보이지않은 형태로도 사용가능

  스마트폰은 화면전환이 필요하지만 태블릿의 경우 화면이 크기 때문에 화면전환보다 하나의 화면에 다 보여야함 

프래그먼트를 사용하여 독립적으로 동작하도록 만든다면 쉽게 구현이 가능하다.

![](../.gitbook/assets/activity_vs_fragment.png)

## 프래그먼트 생성 및 추가 

### **사용자 인터페이스 추가 \(&lt;fragment&gt;\)**

![&amp;lt;fragment&amp;gt; &#xC0AC;&#xC6A9;](../.gitbook/assets/add_ui_fragment.png)

### **사용자 인터페이스 추가 \(java\)**

![](../.gitbook/assets/add_ui_fragment_java.png)

![](../.gitbook/assets/add_ui_fragment_java_2.png)

## 프래그먼트 트랜잭션 수행 

commit\(\)이전의 addToBackStack\(null\) 을 통해 이전상태\(예시에서 교체 트랜잭션\)를 백 스택에 보존한다.

사용자가 Back 버튼을 누름으로써 트랜잭션을 되돌리고 이전 프래그먼트를 다시 가져올 수 있다. 

```java
// Create new fragment and transaction
Fragment newFragment = new ExampleFragment();
FragmentTransaction transaction = getFragmentManager().beginTransaction();

// Replace whatever is in the fragment_container view with this fragment,
// and add the transaction to the back stack
transaction.replace(R.id.fragment_container, newFragment);
transaction.addToBackStack(null);

// Commit the transaction
transaction.commit();
```

## 액티비티와의 통신 

프래그먼트는 getActivity\(\)를 사용하여 액티비티의 레이아웃의 뷰와 메서드를 호출 할 수 있다.

getActivity\(\)는 fragment가 시작할 때 가장 먼저 시작되는 onAttach\(\) 에 선언 하는것이 좋다. 

```java
MainActivity activity = (MainActivity) getActivity();
ListView lst = activity.findViewById(R.id.list);
activity.setImage(R.drawable.user);
```

반대로, 액티비티도 FragmentManager로 부터 Fragment를 참초하여 가져올 수 있다.

```java
ExampleFragment fragment = (ExampleFragment) getFragmentManager().findFragmentById(R.id.example_fragment);
```

## 프래그먼트 생명주기 

![](../.gitbook/assets/frament_lifecycle_2.png)

![](../.gitbook/assets/activity_fragment_lifecycle.png)

## 액티비티와 프래그먼트 간 데이터 전달 

데이터 송신 

```text
examFragment examFragment = new examFragment();
Bundle args = new Bundle(); args.putInt("index", index); 
examFragment.setArguments(args);
```

데이터 수신 

```text
int index = getArguments().getParcelable("index");
```

## 예제 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
public class MainActivity extends AppCompatActivity {

    MainFragment mainFragment;
    MenuFragment menuFragment;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mainFragment = new MainFragment();
        menuFragment = new MenuFragment();
//
        Button btnToMain = findViewById(R.id.btn_to_main);
        btnToMain.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //activity_main의 container에 mainFragment 연결
                getSupportFragmentManager().beginTransaction().replace(R.id.container,mainFragment).commit();
            }
        });
        Button btnToMenu = findViewById(R.id.btn_to_menu);
        btnToMenu.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                getSupportFragmentManager().beginTransaction().replace(R.id.container,menuFragment).commit();
            }
        });
    }
    public void onFragmentChange(int index){
        if(index == 0){
            getSupportFragmentManager().beginTransaction().replace(R.id.container,mainFragment).commit();
        }else if (index == 1){
            getSupportFragmentManager().beginTransaction().replace(R.id.container,menuFragment).commit();
        }
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="MainFragment.java" %}
```java
public class MainFragment extends Fragment {

    MainActivity activity;

    @Override
    public void onAttach(Context context) {
        super.onAttach(context);
        activity = (MainActivity) getActivity();
    }

    @Override
    public void onDetach() {
        super.onDetach();
        activity = null;
    }

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        ViewGroup rootView = (ViewGroup) inflater.inflate(R.layout.fragment_main,container,false);

        Button btnToMenu = rootView.findViewById(R.id.btn_to_menu);
        btnToMenu.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                activity.onFragmentChange(1);
            }
        });
        return rootView;
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="MenuFragment.java" %}
```java
public class MenuFragment extends Fragment {
    MainActivity activity;

    @Override
    public void onAttach(Context context) {
        super.onAttach(context);
        activity = (MainActivity) getActivity();
    }

    @Override
    public void onDetach() {
        super.onDetach();
        activity = null;
    }

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        ViewGroup rootView = (ViewGroup) inflater.inflate(R.layout.fragment_menu,container,false);


        Button btnToMain = rootView.findViewById(R.id.btn_to_main);
        btnToMain.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                activity.onFragmentChange(0);
            }
        });
        return rootView;
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="activity\_main.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/btn_to_main"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="메인" />
    <Button
        android:id="@+id/btn_to_menu"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="7dp"
        android:layout_marginLeft="7dp"
        android:layout_toEndOf="@+id/btn_to_main"
        android:layout_toRightOf="@+id/btn_to_main"
        android:text="메뉴" />
    <FrameLayout

        android:id="@+id/container"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@+id/btn_to_main">

        <!--<fragment-->
            <!--android:id="@+id/fragment_main"-->
            <!--android:name="com.example.examfragment.MainFragment"-->
            <!--android:layout_width="match_parent"-->
            <!--android:layout_height="match_parent" />-->

    </FrameLayout>


</RelativeLayout>
```
{% endcode-tabs-item %}

{% code-tabs-item title="fragment\_main.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/holo_orange_dark"
    android:orientation="vertical">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="프래그먼트 1"
        />

    <Button
        android:id="@+id/btn_to_menu"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="메뉴화면으로"/>
</LinearLayout>
```
{% endcode-tabs-item %}

{% code-tabs-item title="fragment\_menu.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/holo_blue_dark"
    android:orientation="vertical">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="프래그먼트 2" />

    <Button
        android:id="@+id/btn_to_main"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="메인화면으로" />
</LinearLayout>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

![](../.gitbook/assets/fragment.gif)

## 

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17074/" %}






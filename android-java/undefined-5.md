---
description: '#부스트코스'
---

# Extra

## 플래그 

**Intent.FLAG\_ACTIVITY\_NEW\_TASK** 

* 액티비티들을 관리하는 태스크\(TASK\) 객체를 새로 만듦.
* 브로드캐스트 수신자나 서비스의 경우 화면이 없기 때문에 새로운 화면을 띄워야 하므로 이 플래그 사용. 

**Intent.FLAG\_ACTIVITY\_SINGLE\_TOP**

* 같은 액티비티인경우 하나만 띄우도록 함. 

**Intent.FLAG\_ACTIVITY\_CLEAR\_TOP**

* 액티비티 스택에 액티비티A -&gt; 액티비티B 인 상태에서 액티비티A가 새로 추가된경우 이 액티비티 A에 쌓인 액티비티들을 제거하는 역할은 함.

{% embed url="https://developer.android.com/guide/components/activities/tasks-and-back-stack\#IntentFlagsForTasks" %}



## 액티비티에서 인텐트를 전달받는 두가지 경우

플래그 없이 인텐트전달 : onCreate\(\) -&gt; getInent\(\) 

플래그를 사용한 인텐트 전달\(액티비티 재사용 시\) : onNewIntent\(\)

## 부가데이터 전달

putExtra\(\), putParcelableArrayListExtra\(\) 을 통해 데이터를 전달하며  

getIntExtra\(\), getStringExtra\(\), getSerializeableExtra\(\), getParcelableArrayListExtra\(\) 으로 데이터를 전달 받는다.

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
Intent intent = new Intent(getApplicationContext(), MenuActivity.class);
ArrayList<String> names = new ArrayList<String>();
names.add("Tom");
names.add("John");
intent.putExtra("names", names);

SimpleData data = new SimpleData(100,"Hello");
intent.putExtra("data",data);
startActivityForResult(intent, 101);
```
{% endcode-tabs-item %}

{% code-tabs-item title="MenuActivity.java" %}
```java
Intent passedIntent = getIntent();

 processIntent(passedIntent);

private void processIntent(Intent intent) {
    if(intent !=null){
        ArrayList<String> names = (ArrayList<String>) intent.getSerializableExtra("names");
        if(names != null){
            Toast.makeText(getApplicationContext(),"전달받은 이름 리스트 개수 : " + names.size(),Toast.LENGTH_LONG).show();
        }

        SimpleData data = intent.getParcelableExtra("data");
        if(data !=null){
            Toast.makeText(getApplicationContext(),"전달받은 SimpleData : " +data.message,Toast.LENGTH_LONG).show();
        }

    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 기본 자료형 데이터\(int, String, ...\)

{% code-tabs %}
{% code-tabs-item title="FirstActivity.java" %}
```java
Intent intent = new Intent(getApplicationContext(),MenuActivity.class);
int number = 1;
String data = "Hello";
intent.putExtra("number",number);
intent.putExtra("data",data);
```
{% endcode-tabs-item %}

{% code-tabs-item title="SecondActivity.java" %}
```java
Intent intent = getIntent();
int count = intent.getIntExtra("number",0);
String data = intent.getStringExtra("data");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### ArrayList

{% code-tabs %}
{% code-tabs-item title="FirstActivity.java" %}
```java
Intent intent = new Intent(getApplicationContext(),MenuActivity.class);
ArrayList<String> dataArrayList = new ArrayList<String>();
dataArrayList.add("A");
dataArrayList.add("B");
dataArrayList.add("C");

intent.putExtra("dataArrayList",dataArrayList);
```
{% endcode-tabs-item %}

{% code-tabs-item title="SecondActivity.java" %}
```java
Intent intent = getIntent();
ArrayList<String> names = (ArrayList<String>) intent.getSerializableExtra("names");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 객체를 전달할 수 있는 Parcelable

{% code-tabs %}
{% code-tabs-item title="FirstActivity.java" %}
```java
Intent intent = new Intent(getApplicationContext(),MenuActivity.class);
SimpleData data = new SimpleData();
intent.putExtra("data",data);
```
{% endcode-tabs-item %}

{% code-tabs-item title="SecondActivity.java" %}
```java
Intent intent = getIntent();
SimpleData data = intent.getParcelableExtra("data");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### ArrayList Parcelable

{% code-tabs %}
{% code-tabs-item title="FirstActivity.java" %}
```java
Intent intent = new Intent(getApplicationContext(),MenuActivity.class);
ArrayList<SimpleData> simpleDataArrayList = new ArrayList<SimpleData>();
intent.putParcelableArrayListExtra("simpleDataArrayList",simpleDataArrayList);
```
{% endcode-tabs-item %}

{% code-tabs-item title="SecondActivity.java" %}
```java
Intent intent = getIntent();
ArrayList<SimpleData> names = (ArrayList<SimpleData>) intent.getParcelableArrayListExtra("simpleDataArrayList");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17066/" %}




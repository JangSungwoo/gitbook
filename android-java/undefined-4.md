---
description: '#부스트코스'
---

# Activity

## 안드로이드 앱을 구성하는 네가지 구성요소

* **Activity**
* **Service**
* **Broadcast Receiver**
* **Content Provider**

안드로이드 앱을 구성하는 구성요소 중에 Activity에 대해서 알아보자.

### 액티비티 화면 전환 

#### MainActivity -&gt; MenuActivity 로 이동

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
Intent intent = new Intent(getApplicationContext(),MenuActivity.class);
startActivityForResult(intent,101);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### MenuActivity -&gt; MainActivity 로 데이터 전송 후 액티비티 종료 

{% code-tabs %}
{% code-tabs-item title="MenuAcitivity.java" %}
```java
Intent intent = new Intent();
intent.putExtra("name","mike");
setResult(Activity.RESULT_OK,intent);
finish();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
**액티비티를 종료하는 방법** 

일반적으로 액티비티는 스택형식으로 쌓이기 때문에 액티비티를 종료할 경우 finish\(\) 메소드를 통해 액티비티가 종료되고 이전 액티비티가 나타나게 된다.
{% endhint %}

#### MenuActivity로 부터 전송 데이터 MainActivity에서 수신   

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    if(requestCode == 101){
       String name = data.getStringExtra("name");
       Toast.makeText(getApplicationContext(),"메뉴화면으로부터 응답 :" + name ,Toast.LENGTH_LONG).show();
    }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17064/" %}




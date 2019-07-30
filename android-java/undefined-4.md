---
description: '#부스트코스'
---

# Activity

## 안드로이드 앱을 구성하는 네가지 구성요소

* **Activity**
* **Service**
* **Broadcast Receiver**
* **Content Provider**

### 액티비티 화면 전환 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
Intent intent = new Intent(getApplicationContext(),MenuActivity.class);
startActivityForResult(intent,101);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

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


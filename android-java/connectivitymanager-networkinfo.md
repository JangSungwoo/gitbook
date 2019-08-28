---
description: '#부스트코스'
---

# ConnectivityManager, NetworkInfo

### 네트워크 상태 접근 권한 

```markup
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### ConnectivityManager 객체 생성

{% code-tabs %}
{% code-tabs-item title="NetworkStatus.java" %}
```java
ConnectivityManager manager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 네트워크 정보 가져오기 

{% code-tabs %}
{% code-tabs-item title="NetworkStatus.java" %}
```java
NetworkInfo networkInfo = manager.getActiveNetworkInfo();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 네트워크 타입 리턴

{% code-tabs %}
{% code-tabs-item title="NetworkStatus.java" %}
```java
if(networkInfo !=null){
            int type = networkInfo.getType();
            if(type == ConnectivityManager.TYPE_MOBILE){
                return TYPE_MOBILE;
            }else if(type == ConnectivityManager.TYPE_WIFI){
                return TYPE_WIFI;
            }
        }
        return TYPE_NOT_CONNECTED;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 전체 소스 코드 

{% code-tabs %}
{% code-tabs-item title="NetworkStatus.java" %}
```java
public class NetworkStatus {
    public static final int TYPE_WIFI = 1;
    public static final int TYPE_MOBILE = 2;
    public static final int TYPE_NOT_CONNECTED = 3;
    public static int getConnectivityStatus(Context context){
        ConnectivityManager manager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
        NetworkInfo networkInfo = manager.getActiveNetworkInfo();
        if(networkInfo !=null){
            int type = networkInfo.getType();
            if(type == ConnectivityManager.TYPE_MOBILE){
                return TYPE_MOBILE;
            }else if(type == ConnectivityManager.TYPE_WIFI){
                return TYPE_WIFI;
            }
        }
        return TYPE_NOT_CONNECTED;
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/20491/" %}




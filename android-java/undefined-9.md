---
description: '#부스트코스'
---

# Permission

## 일반 권한과 위험권한\(마시멜로 API23부터\)

#### 일반 권한 : 설치 시 사용자의 설치 수락을 통해 사용자 승인을 받음 

#### 위험 권한 : 실행 시 사용자의 위험권한 허용을 통해 사용자 승인을 받음 

![&#xC77C;&#xBC18; &#xAD8C;&#xD55C;&#xACFC; &#xC704;&#xD5D8; &#xAD8C;&#xD55C;](../.gitbook/assets/permission_normal_danger.png)

## 위험 권한의 종류 

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Location</td>
      <td style="text-align:left">
        <p>ACCESS_FINE_LOCATION</p>
        <p>ACCESS_COARSE_LOCATION</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CAMERA</td>
      <td style="text-align:left">CAMERA</td>
    </tr>
    <tr>
      <td style="text-align:left">MICROPHONE</td>
      <td style="text-align:left">RECORD_AUDIO</td>
    </tr>
    <tr>
      <td style="text-align:left">CONTACTS</td>
      <td style="text-align:left">
        <p>READ_CONTACTS</p>
        <p>WRITE_CONTACTS</p>
        <p>GET_ACCOUNTS</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PHONE</td>
      <td style="text-align:left">
        <p>READ_PHONE_STATE</p>
        <p>CALL_PHONE</p>
        <p>READ_CALL_LOG</p>
        <p>WRITE_CALL_LOG</p>
        <p>ADD_VOICEMAIL</p>
        <p>USE_SIP</p>
        <p>PROCESS_OUTGOING_CALLS</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SMS</td>
      <td style="text-align:left">
        <p>SEND_SMS</p>
        <p>RECEVIE_SMS</p>
        <p>RECEIVE_WAP_PUSH</p>
        <p>RECEIVE_MMS</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CALENDAR</td>
      <td style="text-align:left">
        <p>READ_CALENDAR</p>
        <p>WRITE_CALENDAR</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SENSORS</td>
      <td style="text-align:left">BODY_SENSORS</td>
    </tr>
    <tr>
      <td style="text-align:left">STORAGE</td>
      <td style="text-align:left">
        <p>READ_EXTERNAL_STORAGE</p>
        <p>WRITE_EXTERNAL_STORAGE</p>
      </td>
    </tr>
  </tbody>
</table>## 위험 권한 부여 방법 

* ContextCompat.checkSelfPermission : 권한 부여 여부
* ActivityCompat.shouldShowRequestPermissionRationale : 해당 권한 거부\(true\), 다시묻지않음 또는 기기에서 해당 권한 금지 시 false 반
* requestPermission : 권한 요청

권한이 여러개인경우 String\[\] 로 값을 넣어 `requestPermission()` 을 통해 넘겨준다.

{% code title="MainActivity.java" %}
```java
String[] permissions = {
        Manifest.permission.READ_EXTERNAL_STORAGE,
        Manifest.permission.WRITE_EXTERNAL_STORAGE,
        Manifest.permission.RECORD_AUDIO,
};
initPermission(permissions,REQUEST_CODE_READ_EXTERNAL_STORAGE);
initPermission(permissions,REQUEST_CODE_WRITE_EXTERNAL_STORAGE);
initPermission(permissions,REQUEST_CODE_RECORD_AUDIO);
```
{% endcode %}

```java
private void initPermission(String[] permissions, int requestCode) {
            //Manifest의 권한 확인
            int permissionCheck = ContextCompat.checkSelfPermission(this, permissions[requestCode-1] );
            //권한 여부 확인
            if (permissionCheck == PackageManager.PERMISSION_GRANTED) {
                Toast.makeText(this, "권한 주어져 있음.", Toast.LENGTH_LONG).show();
            } else {
                Toast.makeText(this, "권한 없음", Toast.LENGTH_LONG).show();
                if (ActivityCompat.shouldShowRequestPermissionRationale(this, permissions[requestCode-1])) {
                    Toast.makeText(this, "권한 설명 필요함", Toast.LENGTH_LONG).show();
                } else {
                    //권한 요청
                    ActivityCompat.requestPermissions(this, permissions, requestCode);
                }
            }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
//        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        switch (requestCode) {
            case REQUEST_CODE_READ_EXTERNAL_STORAGE:
                if (grantResults.length > 0) {
                    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[0] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
                break;
            case REQUEST_CODE_WRITE_EXTERNAL_STORAGE:
                if (grantResults.length > 0) {
                    if (grantResults[1] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[1] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
                break;
            case REQUEST_CODE_RECORD_AUDIO:
                if (grantResults.length > 0) {
                    if (grantResults[2] == PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한을 사용자가 승인함", Toast.LENGTH_LONG).show();
                    } else if (grantResults[2] == PackageManager.PERMISSION_DENIED) {
                        Toast.makeText(this, "권한을 사용자가 거부함", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(this, "권한을 부여받지 못함", Toast.LENGTH_LONG).show();
                }
                break;

        }
    }

```

{% hint style="info" %}
build.gradle 파일의 targetSdkVersion을 23미만으로 설정을 할 경우 위험권한이 자동으로 부여된다. targetSdkVersion 이 23이상인경우 권한 부여 요청 대화상자가 뜨며 사용자가 허용을 한다면 정상적인 동작을 하게 된다. 
{% endhint %}

{% embed url="https://developer.android.com/guide/topics/security/permissions.html?hl=ko" %}



{% embed url="https://edwith.org/boostcourse-android/lecture/22591/" %}




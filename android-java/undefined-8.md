---
description: '#부스트코스'
---

# BroadCastReceiver

## 브로드 캐스팅 이란?

**: 메세지를 여러 대상에게 전달 하는 것**

## 브로드 캐스트 수신자 

* 애플리케이션이 글로벌 이벤트\(global event\)를 받아서 처리하려면 브로드캐스트 수신자 등록
* 글로벌 이벤트란 "전화가 왔습니다","문자 메세지가 도착했습니다"와 같이 안드로이드 시스템 전체에 보내지는 이벤트
* 브로드 캐스트 수신자는 인텐트필터를 포함하며, 매니페스트 파일에 등록함으로써 인텐트를 받을 준비를 함
* 수신자가 매니페스트 파일에 등록되었다면 따로 시작시키지 않아도 됨 
* 애플리케이션 컨텍스트 클래스의 registerReceiver 메소드를 이용하면 런타임 시에도 수신자를 등록할 수 있음 
* 서비스처럼 브로드캐스트 수신자도 UI가 없음  

## 브로드 캐스트의 구분 

### 인텐트와 브로드 캐스트 

* 인텐트를 이용해서 액티비티를 실행하면 포그라운드\(foreground\)로 실행되어 사용자에게 보여지지만 브로드 캐스트를 이용해서 처리하면 백그라운드\(background\)로 동작하므로 사용자가 모름 
* 인텐트를 받으면 onReceive\(\) 메소드가 자동으로 호출됨 

### 브로드 캐스트의 구분 

* 일반 브로드캐스트 \(sendBroadcast\(\) 메소드로 호출\) 

         -  비동기적으로 실행되며 모든 수신자는 순서없이 실행됨. \(때로는 동시에 실행됨\) 효율적이지만 한 수 신자의 처리 결과를 다른 수신자가 이용할 수 없고 중간에 취소불가 

* 순차브로드 캐스트\(sendOrderedBroadcase\(\) 메소드로 호출\)

          - 한 번에 하나의 수신자에만 전달되므로 순서대로 실행됨. 중간에 취소하면 그 다음 수신자는 받지못함. 수신자가 실행되는 순서는 인텐트필터의 속성으로 정할 수 있음. 순서가 같으면 임의로 실행됨. 

## 브로드캐스트 수신자 예제 

브로드 캐스트의 메세지를 받기위해서는 브로드캐스트 수신자\(BroadCastReceiver\)를 등록해야한다.

가장 대표적인 SMS를 예로 들어보자. 아래 예제에서는 커스텀 SMS Activity를 띄우도록 하였다.

![](../.gitbook/assets/broadcast_sms.png)

### 1\) 우선 BroadCastRecevier를 생성한다.

{% code-tabs %}
{% code-tabs-item title="SmsReceiver.java" %}
```java
public class SmsReceiver extends BroadcastReceiver {
    private static final String TAG = "SmsReceiver";

    private  static SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm");

    @Override
    public void onReceive(Context context, Intent intent) {
        if(intent.getAction() =="android.provider.Telephony.SMS_RECEIVED"){
            Log.d(TAG, "OnReceive() 호출됨");
        }
     }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

intent-filter로 지정한 action을 비교하여 특정 인텐트만 처리할 수 있다.  

```java
intent.getAction() =="android.provider.Telephony.SMS_RECEIVED"
```

### 2\) AndroidManifest 의 intent-filter에 action을 설정한다.

{% code-tabs %}
{% code-tabs-item title="AndroidManifest.xml" %}
```markup
<receiver
    android:name=".SmsReceiver"
    android:enabled="true">
    <intent-filter android:priority="1">
        <action android:name="android.provider.Telephony.SMS_RECEIVED" />
    </intent-filter>
</receiver>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

intent-filter 의 action을 통해 지정한 인텐트만 받겠다고 지정을 할 수 있다. 



### 3\) AndroidManifest SMS 권한을 설정한다. 

```markup
<uses-permission android:name="android.permission.RECEIVE_SMS" />
```

안드로이드 버전이 22 이하인경우 위험권한을 자동으로 설정하지만 버전 23 부터는 사용자에게 위험권한 승인을 받아야 정상적인 기능을 수행할 수 있다. 

### 4\) SmsRecevier를 통해 수신된 intent로 부터 데이터를 수신 및 처리 

```java
public class SmsReceiver extends BroadcastReceiver {
    private static final String TAG = "SmsReceiver";

    private static SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm");

    @Override
    public void onReceive(Context context, Intent intent) {
      if(intent.getAction() =="android.provider.Telephony.SMS_RECEIVED") {
            Log.d(TAG, "OnReceive() 호출됨");

            Bundle bundle = intent.getExtras();
            SmsMessage[] message = parseSmsMessage(bundle);
            if (message.length > 0) {
                String sender = message[0].getOriginatingAddress();
                Log.d(TAG, "sender : " + sender);

                String contents = message[0].getMessageBody().toString();
                Log.d(TAG, "contents : " + contents);

                Date receiverDate = new Date(message[0].getTimestampMillis());
                Log.d(TAG, "received date : " + receiverDate);
                //SmsActivity로 데이터를 전달한다. 
                sendToActivity(context, sender, contents, receiverDate);
            }
        }

    }

    private void sendToActivity(Context context, String sender, String contents, Date receiverDate) {
        Intent intent = new Intent(context,SmsActivity.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK
                        |Intent.FLAG_ACTIVITY_SINGLE_TOP
                        |Intent.FLAG_ACTIVITY_CLEAR_TOP);
        intent.putExtra("sender",sender);
        intent.putExtra("contents",contents);
        intent.putExtra("receivedDate",format.format(receiverDate));

        context.startActivity(intent);
    }

    private SmsMessage[] parseSmsMessage(Bundle bundle) {
        Object[] objs = (Object[]) bundle.get("pdus");
        SmsMessage[] messages = new SmsMessage[objs.length];
        for (int i = 0; i < objs.length; i++) {
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                String format = bundle.getString("format");
                messages[i] = SmsMessage.createFromPdu((byte[]) objs[i], format);
            } else {
                messages[i] = SmsMessage.createFromPdu((byte[]) objs[i]);

            }
        }
        return messages;
    }
}

```

다음과 같이 인텐트의 정보를 가져올 수 있다.

```java
Bundle bundle = intent.getExtras();
```

인텐트 데이터를 SMS 형식으로 변환해야 한다. 

```java
SmsMessage[] message = parseSmsMessage(bundle);
```

```java
private SmsMessage[] parseSmsMessage(Bundle bundle) {
        Object[] objs = (Object[]) bundle.get("pdus");
        SmsMessage[] messages = new SmsMessage[objs.length];
        for (int i = 0; i < objs.length; i++) {
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                String format = bundle.getString("format");
                messages[i] = SmsMessage.createFromPdu((byte[]) objs[i], format);
            } else {
                messages[i] = SmsMessage.createFromPdu((byte[]) objs[i]);

            }
        }
    return messages;
}
```

{% hint style="info" %}
pdus란?

SMS를 처리하는 국제 프로토콜 
{% endhint %}

다음 함수를 생성하여 SmsActivity로 데이터를 보낸다 

```java
sendToActivity(context,sender,contents,receiverDate);
```

### 5\) SMS Activity를 생성한다.

```java
public class SmsActivity extends AppCompatActivity {

    EditText edtSender;
    EditText edtContents;
    EditText edtReceivedDate;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sms);

        edtSender = findViewById(R.id.edt_sender);
        edtContents = findViewById(R.id.edt_contents);
        edtReceivedDate = findViewById(R.id.edt_receiving_time);

        Button btnSend = findViewById(R.id.btn_send);

        btnSend.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish();
            }
        });

        Intent passedIntent = getIntent();
        processCommand(passedIntent);
    }

    @Override
    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
    }

    private void processCommand(Intent intent) {
        if(intent != null){
            String sender = intent.getStringExtra("sender");
            String contents = intent.getStringExtra("contents");
            String receivedDate = intent.getStringExtra("receivedDate");

            edtSender.setText(sender);
            edtContents.setText(contents);
            edtReceivedDate.setText(receivedDate);
        }
    }
}
```

![](../.gitbook/assets/broadcast_sms.gif)

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17069/" %}




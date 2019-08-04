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
        //if(intent.getAction() =="android.provider.Telephony.SMS_RECEIVED"){
        Log.d(TAG, "OnReceive() 호출됨");
        //}

        Bundle bundle = intent.getExtras();
        SmsMessage[] message = parseSmsMessage(bundle);
        if (message.length > 0){
            String sender = message[0].getOriginatingAddress();
            Log.d(TAG,"sender : " + sender);

            String contents = message[0].getMessageBody().toString();
            Log.d(TAG, "contents : " + contents);

            Date receiverDate = new Date(message[0].getTimestampMillis());
            Log.d(TAG,"received date : " + receiverDate);
            //smsActivity로 데이터를 보냄 
            sendToActivity(context,sender,contents,receiverDate);
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
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
pdus란?

SMS를 처리하는 국제 프로토콜 
{% endhint %}

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

### 3\) AndroidManifest SMS 권한을 설정한다. 

```markup
<uses-permission android:name="android.permission.RECEIVE_SMS" />
```

### 4\) SMS Activity를 생성한다.

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




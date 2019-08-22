---
description: '#부스트코스'
---

# Request To Web

### URLConnection 객체

```text
[API]
public URLConnection openConnection()
* HttpURLConnection 객체로 형변환(casting)하여 사
```

### 요청 관련 메소드

```text
[API]
public void setRequestMethod(String method)
public void setRequestProperty(String field, String newValue)
```

{% hint style="info" %}
okhttp, volley, retrofit 을 사용하면 간단하게 웹으로 요청이 가능함 
{% endhint %}

### RequestThread 생성

1\) HttpURLConnection을 사용하여 url에 연결을 한다. 

2\) 연결이 정상적으로 되었다면 연결시간, 요청메소드, 입력 및 출력 여부를 설정한다.

3\) 요청 코드를 받아서 처리하려면 getResponseCode\(\) 를 사용하여 처리한다.

4\) url 로부터 전달받은 응답데이터는 getInputStream\(\)의 형태로 BufferedReader 객체를 생성한다.  

5\) readLine\(\) 으로 값을 가져와서 처리한다. 

6\) 통신이 완료되었다면 BufferedReader 와 HttpURLConnection를  close한다. 

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
class RequestThread extends Thread {
        public void run() {
            String urlStr = edtUrl.getText().toString();
            try {
                URL url = new URL(urlStr);
                HttpURLConnection conn = (HttpURLConnection) url.openConnection();
                if (conn != null) {
                    conn.setConnectTimeout(10000);
                    conn.setRequestMethod("GET");
                    conn.setDoInput(true);
                    conn.setDoOutput(true);

                    int resCode = conn.getResponseCode();

                    BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream()));
                    String line = null;

                    while (true) {
                        line = reader.readLine();
                        if (line == null) {
                            break;
                        }

                        println(line);
                    }
                    reader.close();
                    conn.disconnect();
                }
            } catch (MalformedURLException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 요청 스레드 시작

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
RequestThread thread = new RequestThread();
                thread.start();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 권한 부여 

```markup
<uses-permission android:name="android.permission.INTERNET" />
```

### 전체 소스코드

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
public class MainActivity extends AppCompatActivity {
    EditText edtUrl;
    Button btnRequest;
    TextView txtResponse;

    Handler handler = new Handler();
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        edtUrl = findViewById(R.id.edt_url);
        txtResponse = findViewById(R.id.txt_response);
        btnRequest = findViewById(R.id.btn_request);
        btnRequest.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                RequestThread thread = new RequestThread();
                thread.start();
            }
        });
    }

    class RequestThread extends Thread {
        public void run() {
            String urlStr = edtUrl.getText().toString();
            try {
                URL url = new URL(urlStr);
                HttpURLConnection conn = (HttpURLConnection) url.openConnection();
                if (conn != null) {
                    conn.setConnectTimeout(10000);
                    conn.setRequestMethod("GET");
                    conn.setDoInput(true);
                    conn.setDoOutput(true);

                    int resCode = conn.getResponseCode();

                    BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream()));
                    String line = null;

                    while (true) {
                        line = reader.readLine();
                        if (line == null) {
                            break;
                        }

                        println(line);
                    }
                    reader.close();
                    conn.disconnect();
                }
            } catch (MalformedURLException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    private void println(final String data) {
        handler.post(new Runnable() {
            @Override
            public void run() {
                txtResponse.append(data + "\n");

            }
        });
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% embed url="https://developer.android.com/training/basics/network-ops/connecting.html" %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/20488/" %}




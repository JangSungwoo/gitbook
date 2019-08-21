---
description: '#부스트코스'
---

# Thread

## 멀티스레드 

![](../.gitbook/assets/thread.png)

## 표준 자바에서 스레드 사용 방법 

예시 

```text
running = true;
Thread thread1 = new BackgroundThread();
thread1.start();

class BackgroundThread extends Thread{
    public void run(){
        while(running){
            try{
                Thread.sleep(1000);
                value++;
            }catch(InterruptedExceoption ex){
                Log.e("SampleJavaThread","Exception in Thread.",ex);
            }
        }
    }
}
```

## 핸들러 사용하기

![&#xD578;&#xB4E4;&#xB7EC;&#xB97C; &#xC0AC;&#xC6A9;&#xD560; &#xB54C; &#xD544;&#xC694;&#xD55C; &#xC138;&#xAC00;&#xC9C0; &#xB2E8;&#xACC4; ](../.gitbook/assets/handler.png)

### 1\) obtainMessage\(\)

* 메세지 객체 리턴 

### 2\) sendMessage\(\)

* 메세지큐에 넣음 

### 3\) handleMessage\(\)

* 메소드에 정의된 기능이 수행됨 
* 코드가 수행되는 위치는 새로 만든 스레드가 아닌 메인스레드에서 수행됨 

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17086/" %}




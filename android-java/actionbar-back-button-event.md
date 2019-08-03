# ActionBar Back Button Event

일반적으로 뒤로가기 버튼은 두가지가 있다.

* 디바이스 자체에서의 뒤로가기
* ActionBar에서의 뒤로가기

두가지를 사용했을때 호출되는 오버라이드 메소드들에 대해 알아보자

## 디바이스에서의 뒤로가기

```java
@Override
public void onBackPressed() {
    super.onBackPressed();
    //여기에 입력 
}
```

## ActionBar에서의 뒤로가기

```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case android.R.id.home:
            //여기에 입력 
            break;
    }
    return true;
}
```












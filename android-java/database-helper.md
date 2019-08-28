---
description: '#부스트코스'
---

# DataBase , Helper

## 헬퍼 클래스 

```text
public SQLiteOpenHelper(Context context, String name, SQLiteDatabase.CursorFactory factory, int version) 
```

### onCreate\(\)

* 데이터베이스가 처음 만들어질 때 호출되므로 테이블을 생성하는 등 초기화하는 코드를 수행 

### onOpen\(\)

* 
### onUpgrade\(\)

* 테이블이 변경되어야 하는 등 단말에 저장된 데이터베이스의 구조가 바뀌어야 하는 경우에 사용 
* 테이블을 변경하기위한 ALTER 문 등을 넣을 수 있으며 이미 저장되어 있는 데이터를 다른곳에 복사했다가 새로 테이블을 만들고 그 테이블에 넣어주는 방식으로도 처리 가능 

{% hint style="warning" %}
SQLiteOpenHelper 사용시 getWritableDatabase\(\) 메소드를 사용하더라도 

동일한 이름의 db가 있다면 onCreate\( \) 가 호출되지 않는다.
{% endhint %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17121/" %}




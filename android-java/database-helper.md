---
description: '#부스트코스'
---

# DataBase , Helper

## 데이터베이스 헬퍼를 사용하는 이유?

**데이터베이스의 테이블 구조를 변경해야 하는경우 헬퍼클래스를 사용하여 생성, 오픈, 업그레이드, 다운그레이드를 할 때 유용하다.** 

## 헬퍼 클래스 

```text
public SQLiteOpenHelper(Context context, String name, SQLiteDatabase.CursorFactory factory, int version) 
```

### onCreate\(\)

* 데이터베이스가 처음 만들어질 때 호출되므로 테이블을 생성하는 등 초기화하는 코드를 수행 

### onOpen\(\)

* 데이터베이스 스키마가 생성되는 connection 된 후에 호출된다. 

### onUpgrade\(\)

* 테이블이 변경되어야 하는 등 단말에 저장된 데이터베이스의 구조가 바뀌어야 하는 경우에 사용 
* 테이블을 변경하기위한 ALTER 문 등을 넣을 수 있으며 이미 저장되어 있는 데이터를 다른곳에 복사했다가 새로 테이블을 만들고 그 테이블에 넣어주는 방식으로도 처리 가능 

{% hint style="warning" %}
SQLiteOpenHelper 사용시 getWritableDatabase\(\) 메소드를 사용하더라도 

동일한 이름의 db가 있다면 onCreate\( \) 가 호출되지 않는다.
{% endhint %}

### 헬퍼 사용

```java
DatabaseHelper helper = new DatabaseHelper(context, databaseName, null, 1);
database = helper.getWritableDatabase();
```

getWriteableDatabase\(\)는 데이터베이스를 읽고 쓰기위해서 설정하는 메소드이다. 

{% embed url="https://developer.android.com/training/data-storage/room/index.html" %}

{% embed url="https://gyjmobile.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%95%B1-%EB%9F%B0%EC%B9%AD%ED%9B%84-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EB%B3%80%EA%B2%BD%EC%8B%9C-%EC%A3%BC%EC%9D%98%ED%95%A0%EC%A0%90" %}

{% embed url="https://developer.android.com/guide/topics/providers/content-provider-creating.html?hl=ko" %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17121/" %}




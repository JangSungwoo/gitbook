---
description: '#부스트코스'
---

# DataBase, Table

## 모바일 데이터베이스 

* 설정 정보 
* 파일 사용 
* 데이터베이스 \(많은 데이터를 체계적으로 관리\) 

### 데이터베이스 

* 여러 개의 테이블을 담고 있는 하나의 그릇 역할 

### 데이터베이스 단계 

1\) 데이터 베이스 생성 

2\) 테이블 생성 

3\) 레코드 추가

4\) 데이터 조회 

### SQLite 

* 오픈소스로 만들어진 파일 기반의 데이터베이스. 
* 용량이 적고 가볍게 동작, 관계형 데이터베이스를 위한 SQL 실행 가능하여 광범위하게 사용. 



### 데이터베이스 열거나 삭제 

```java
public abstract SQLiteDatabase openOrCreateDatabase(String name, int mode, SQLiteDatabase.CursorFactory factory)
public abstract boolean deleteDatabase(String name)
```

### 테이블 생성 

```java
private void createTable(String name) {
    println(“creating table [" + name + "].");
 
    db.execSQL("create table " + name + "(" 
        + " _id integer PRIMARY KEY autoincrement, " 
        + " name text, "
        + " age integer, "
        + " phone text);" 
    );
    tableCreated = true;
}
```

{% hint style="info" %}
PRIMARY KEY : 기본키 

autoincrement : 레코드 증가시 자동증가 
{% endhint %}

### 칼럼 타입 

| 칼럼 타입 | 설명  |
| :--- | :--- |
| text, varchar | 문자열  |
| smallint, integer  | 정수 \(2바이트 또는 4바이트\)  |
| real, float, double  | 부동소수 \(4바이트 또는 8바이트\)  |
| boolean  | true 또는 false  |
| date, time, timestamp | 시간 \(날짜, 시간, 날짜+시간\)  |
| blob, binary | 바이너리  |

{% hint style="info" %}
[칼럼 타입](https://www.sqlite.org/datatype3.html) 자세한 정
{% endhint %}

### SQL 실행 메소드 

* create, insert, delete 등 결과데이터가 없는 SQL문 

```java
public void execSQL(String sql) throws SQLException 
```

* select 와 같이 조회에 따른 결과 데이터가 있는 SQL문 

```java
public cursor rawQuery(String sql) throws SQLException 
```



{% embed url="https://www.edwith.org/boostcourse-android/lecture/17119/" %}




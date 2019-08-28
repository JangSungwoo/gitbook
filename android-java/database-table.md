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



### 데이터베이스 열거나 삭제 

```java
public abstract SQLiteDatabase openOrCreateDatabase(String name, int mode, SQLiteDatabase.CursorFactory factory)
public abstract boolean deleteDatabase(String name)
```

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




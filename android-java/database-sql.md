---
description: '#부스트코스'
---

# DataBase, SQL

## DataBase 

데이터가 저장된 저장소. 

### 관계형 데이터 베이스 

**키와 값들의 간단한 관계를 테이블화 시킨 매우 간단한 원칙의 전산정보 데이터베이스.** 

실무에서는 MySQL, Oracle 과 같은 관계형 데이터 베이스를 많이 볼 수 있음 

### 데이터베이스 4단계 

1단계 Open 

2단계 Table 생성 

3단계 추가

4단계 조회 

## 테이블 

테이블 구조는 다음과 같다. 

![](../.gitbook/assets/database%20%281%29.png)

##  스키마 

데이터베이스를 구성하는 레코드의 크기, 키\(key\)의 정의, 레코드와 레코드의 관계, 검색 방법 등을 정의한  것.

### 테이블 생성 

```text
CREATE TABLE tablename(
    accountNumber    VARCHAR(8) NOT NULL,
    clientID    VARCHAR(40) NOT NULL,
    balance    DOUBLE DEFAULT '0',
    availableBalance DOUBLE DEFAULT '0'
);
```

### 테이블 삭제

```text
DROP TABLE tablename;
```

### 튜플 추가 

```text
INSERT INTO Accounts(accountNumber, balance, accountName) 
VALUES('22222', 100000, 'Ample Rich");
```

### 튜플 갱신 

```text
UPDATE city SET population=40000 WHERE name='Langsaen' AND countrycode='THA';
```

### 튜플 삭제 

```text
DELETE FROM city WHERE population <= 0;
```

### 튜플 조회 

```text
SELECT * FROM city WHERE population > 5000000 
ORDER BY population DESC; 
```

{% embed url="https://ko.wikipedia.org/wiki/%EA%B4%80%EA%B3%84%ED%98%95\_%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4" %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17118/" %}




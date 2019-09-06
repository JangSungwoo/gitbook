# AWS Lambda + DynamoDB

## 기본

1\) AWS Management Console 로그인

## 데이터베이스 설계

### 1\) 테이블 생성 

* 서비스 찾기에서 DynamoDB 선택 
* 지역선택 
* Create table 선택 
* TableName, PrimaryKey 입력 \(예제 : Users, id\) 

### 2\) 레코드 추가 

* Item\(항목\)탭 클릭후 레코드 추가 \(예제에서는 id, firstname, lastname 입력함\)

## 권한 정책 설정

### 1\) IAM 서비스 사용 

* 서비스에서 IAM\(Identity and Access Management\)선택

### 2\) Role 설정 

* Role 탭에서 Create Role 클릭 

#### 2-1\) type 설정 

* AWS Service 

#### **2-2\) 해당 Role를 사용할 서비스 선택** 

*  Lambda선택 후 Next: Permission 클릭

#### 2-3\) Attach permissions policies 설정  

AWSLambdaBasicExecutionRole 검색 및 체크 후 Next: Tag 클릭 

#### 2-4\) Tag 입력 

* tag의 Key입력은 패스

#### 2-5\) Review

* RoleName 입력\(예제: LambdaDynamoDBRole\) 
* Create Role 클릭 

### 3\) 생성한 Role의 policy 설정 

#### 3-1\) 생성한 Role선택후 Add inline policy \(인라인정책추가\) 클릭  

#### 3-2\) Visual editor 의 Service에 DynamoDB 검색 후 선택 

#### 3-3\) Actions에 원하는 함수입력\(예제 :  GetItem, PutItem 추가\)   

#### 3-4\) Resources의 table 설정 

* ARN 추가\(Table의 Overview탭의 ARN 복사하여 붙여넣기\) 

#### 리뷰 정책 생성 리뷰 정책명 \(예제에서는 DynamoReadWriteAccess \) Service에서 Lambda선택 지역확인

## get함수 만들기

Create Function 클릭 함수명 \(예제 getUserData \) Runtime \(예제 Node.js 최신버전 \) Role\(이전에 생성한 기존 Role 사용\) Select a test event 추가 이벤트명 : 함수명과동일하게 index.js 에 get 소스코드 추가 저장후 테스트 응답확인

## put함수 만들기

Create Function 클릭 함수명 \(예제 putUserData \) Runtime \(예제 Node.js 최신버전 \) Role\(이전에 생성한 기존 Role 사용\) Select a test event 추가 이벤트명 : 함수명과동일하게 index.js 에 put 소스코드 추가 저장후 테스트 응답확인


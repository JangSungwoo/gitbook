# AWS \(Lambda + DynamoDB\)

{% embed url="https://www.youtube.com/watch?v=ijyeE-pXFk0" %}

위의 강의를 기반으로 작성되었습니다. 

## 시작 

### 1\) AWS Management Console 로그인

## 데이터베이스 구축 \(DynamoDB\)

### 1\) 테이블 생성 

* 서비스 찾기에서 DynamoDB 선택 
* 지역선택 
* Create table 선택 
* TableName, PrimaryKey 입력 \(예제 : Users, id\) 

### 2\) 레코드 추가 

* Item\(항목\)탭 클릭후 레코드 추가 \(예제에서는 id, firstname, lastname 입력함\)

## 권한 정책 설정\(IAM\)

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

#### 2-6\) Create Role 클릭 

### 3\) 생성한 Role의 policy 설정 

#### 3-1\) 생성한 Role선택후 Add inline policy \(인라인정책추가\) 클릭  

#### 3-2\) Visual editor 의 Service에 DynamoDB 검색 후 선택 

#### 3-3\) Actions에 원하는 함수입력\(예제 :  GetItem, PutItem 추가\)   

#### 3-4\) Resources의 table을 위한정보 설정 

* ARN 추가\(Table의 Overview탭의 ARN 복사하여 붙여넣기\) 

#### 3-5\) Review policy 

### 4\) Review policy 

#### 4-1\) 리뷰 정책명 \(예제에서는 DynamoReadWriteAccess \) 

#### 4-2\) Create policy 클릭  

## AWS Lambda

### 1\) AWS Lambda 사용 

* Service에서 Lambda선택 

### 2\) 지역확인

### 3\) get함수 생성 

#### 3-1\) Create Function 클릭 

* 함수명 \(예제 : getUserData \)
* Runtime \(예제 Node.js 최신버전 \) 
* Role\(이전에 생성한 기존 Role 사용, 예제 : LambdaDynamoDBRole \) 

#### 3-2\) 설정후 Create Function 클릭

#### 3-3\) Select a test event 추가 

* 이벤트명 : 함수명과동일하게 
* index.js 에 get 소스코드 추가 저장후 테스트 응답확인

{% code title="index.js" %}
```javascript
'use strict'
const AWS = require('aws-sdk');

AWS.config.update({region: "us-east-2"});
exports.handler = async (event, context) => {
    const ddb = new AWS.DynamoDB({ apiVersion: "2012-10-08"});
    const documentClient = new AWS.DynamoDB.DocumentClient({ region: "us-east-2"});

    const params = {
        TableName: "Employee",
        Key: {
            id: 3
        }
    }

    try{
        const data = await documentClient.get(params).promise();
        console.log(data);
    }catch(err){
        console.log(err);
    }
}
```
{% endcode %}

### 4\) put함수 생성 

#### 4-1\) Create Function 클릭 

* 함수명 \(예제 : putUserData \)
* Runtime \(예제 Node.js 최신버전 \) 
* Role\(이전에 생성한 기존 Role 사용, 예제 : LambdaDynamoDBRole \) 

#### 4-2\) 설정후 Create Function 클릭

#### 4-3\) Select a test event 추가 

* 이벤트명 : 함수명과동일하게 
* index.js 에 put 소스코드 추가 저장후 테스트 응답확인

{% code title="index.js" %}
```javascript
'use strict'
const AWS = require('aws-sdk');

AWS.config.update({region: "us-east-2"});
exports.handler = async (event, context) => {
    const ddb = new AWS.DynamoDB({ region: "us-east-2"});
    const documentClient = new AWS.DynamoDB.DocumentClient({ service: ddb});

    const params = {
        TableName: "Users",
        Item: {
            id: 3,
            firstname: "Jennifer",
            lastname: "abc@abc.com"
        }
    }

    try{
        const data = await documentClient.put(params).promise();
        console.log(data);
    }catch(err){
        console.log(err);
    }
}
```
{% endcode %}




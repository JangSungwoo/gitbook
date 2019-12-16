# Context

## Context란?

* 애플리케이션 환경에 관한 전역 정보를 접근하기 위한 인터페이스.
* 안드로이드 시스템에서 구현을 제공하는 추상클래스.
* 애플리케이션을 구성하는 리소스들, 클래스들, 액티비티 실행과 브로드캐스팅과 인텐트수신 등의 애플리케이션 레벨 작업의 접근을 허용. 

[Android Developers : Context](https://developer.android.com/reference/android/content/Context) 공식문서에는 위와 같이 명시되어 있다.

### 애플리케이션 환경에 관한 전역정보?

![](../.gitbook/assets/image%20%283%29.png)

위의 사진은 공식문서의 getApplicationContext\(\)에 대한 설명이다.

> 현재 프로세스의 전역 애플리케이션 객체인 하나의 context를 리턴하라.

리눅스 운영체제의 개념을 학습하였다면 Context를 들어보았을 것이다. 프로세스는 문맥교환\(Context Switching\)을 통해 현재 작업 프로세스를 스케쥴링 한다. 

또한 안드로이드도 리눅스 기반 OS이기 때문에 애플리케이션을 실행시키기 위한 프로세스가 필요할 것이고, 그 안에는 애플리케이션을 실행하기 위한 모든정보들이 있을것이다. 안드로이드 4대 컴포넌트도 포함되어있을것이고 리소스들과 클래스들도 포함되어있을 것이다. 

하지만 안드로이드는 ActivityManagerService 

---수정중---


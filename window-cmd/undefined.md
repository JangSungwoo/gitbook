# 배치파일로 폴더에 압축파일 저장

현재폴더의 파일 폴더들을 한꺼번에 백업파일에 저장을 하는 배치파일 프로그램을  만들어보자



```text
@echo off
SET DIRORG=%CD%
@echo %DIRORG%
SET BAKPATH=%DIRORG%\00_Backup%
@echo %BAKPATH%
SET EXTDIR=-ex:"*압축백업정리.bat;00_backup"
@echo %EXTDIR%

FOR /F "tokens=2-4 delims=/ " %%i IN ('date /t') DO SET DATE=%%i-%%j-%%k
FOR /F "tokens=1-3 delims=: " %%i IN ('time /t') DO SET TIME=%%i-%%j-%%k

SET DATETIME=%DATE%-%TIME%
SET DIRBAK=%BAKPATH%\%DATETIME%.zip
@echo %DIRBAK%

"C:\Program Files\Bandizip\Bandizip.exe" a %EXTDIR% %DIRBAK% %DIRORG% 
```

반디집으로 압축을 할 경우 제외할 파일은 이렇게 사용해야한다.

 `-ex:"제외파일1.txt;제외폴더"`

원하는 경로를 치환해서 아래와같이 사용하면 특정파일 및 폴더는 제외하고  현재위치의 파일 및 폴더를 지정한 폴더안에 압축파일을 생성한다.

```text
"C:\Program Files\Bandizip\Bandizip.exe" a %EXTDIR% %DIRBAK% %DIRORG% 
```



{% embed url="https://kr.bandisoft.com/bandizip/help/parameter/" %}

{% embed url="https://m.blog.naver.com/PostView.nhn?blogId=mymizze&logNo=90189250583&proxyReferer=https%3A%2F%2Fwww.google.com%2F" %}




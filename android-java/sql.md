# sql 에서 작은따옴표\( ' \) 처리

다음과 같은경우 작은따옴표\( ' \) 때문에 에러가 발생한다.  

```text
update movie set contents = ' 'Hello' ' where id = 1
```

다음과 같이 작은따옴표를 두개씩 사용해야 한다.  

```text
update movie set contents = ' ''Hello'' ' where id = 1
```


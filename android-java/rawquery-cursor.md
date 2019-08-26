# rawQuery 사용시 cursor 값 처리



```text
Cursor cursor = database.rawQuery(sql, null);
if( cursor != null && cursor.moveToFirst() ) {
    //cursor 에 대한 처리 
}
```


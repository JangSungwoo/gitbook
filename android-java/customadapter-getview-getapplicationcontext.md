# CustomAdapter의 getView에서 getApplicationContext\(\) 가져오는법

```java
@Override
    public View getView(int position, View convertView, ViewGroup parent) {
        CommentItemView view = new CommentItemView(parent.getContext());

        UserItem item = items.get(position);
        view.setTvUserId(item.UserId);

        return view;
    }
```

getApplicationContext\(\)  대신에 parent.getContext\(\)를 사용하면된다.




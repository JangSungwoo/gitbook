# ScrollView 안의 ListView Scroll문제

{% embed url="https://stackoverflow.com/questions/6210895/listview-inside-scrollview-is-not-scrolling-on-android" %}

```java
ListView lv = (ListView)findViewById(R.id.myListView);  // your listview inside scrollview
lv.setOnTouchListener(new ListView.OnTouchListener() {
        @Override
        public boolean onTouch(View v, MotionEvent event) {
            int action = event.getAction();
            switch (action) {
            case MotionEvent.ACTION_DOWN:
                // Disallow ScrollView to intercept touch events.
                v.getParent().requestDisallowInterceptTouchEvent(true);
                break;

            case MotionEvent.ACTION_UP:
                // Allow ScrollView to intercept touch events.
                v.getParent().requestDisallowInterceptTouchEvent(false);
                break;
            }

            // Handle ListView touch events.
            v.onTouchEvent(event);
            return true;
        }
    });
```


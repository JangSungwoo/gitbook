# View disable 하는법



```java
private void setEnabled(ViewGroup layout,boolean state) {
    layout.setEnabled(state);
    for (int i = 0; i < layout.getChildCount(); i++) {
        View child = layout.getChildAt(i);
        if (child instanceof ViewGroup) {
            setEnabled((ViewGroup) child,state);
        } else {
            child.setEnabled(state);
        }
    }
}
```


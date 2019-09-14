# font

## 직접 폰트를 설정하는방법 



```text
Typeface tf = Typeface.createFromAsset(getAssets(), "fonts/gobaaa.ttf");
textView.setTypeface(tf);
```

### 어댑터안에서 

```text
Typeface tf = Typeface.createFromAsset(itemView.getContext().getAssets(), "fonts/gobaaa.ttf");
textView.setTypeface(tf);
```


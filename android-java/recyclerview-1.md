# RecyclerView의 특정아이템 설정하는방법

### RecyclerView의 아이템 RadioButton 클릭

```java
public void selectSoundItem(final int position) {
        recyclerView.getViewTreeObserver().addOnGlobalLayoutListener(new ViewTreeObserver.OnGlobalLayoutListener() {
            @Override
            public void onGlobalLayout() {
                View itemView = recyclerView.getChildAt(position);
                SoundAdapter.ViewHolder holder = (SoundAdapter.ViewHolder) recyclerView.findViewHolderForAdapterPosition(position);
                holder.getRadioBtnSoundItem().setChecked(true);
            }
        });
    }
```


# RecyclerView의 특정아이템 설정하는방법

### RecyclerView의 아이템 RadioButton 클릭

```java
public void selectSoundItem(final int position) {
        recyclerView.getViewTreeObserver().addOnGlobalLayoutListener(new ViewTreeObserver.OnGlobalLayoutListener() {
            @Override
            public void onGlobalLayout() {
                SoundAdapter.ViewHolder holder = (SoundAdapter.ViewHolder) recyclerView.findViewHolderForAdapterPosition(position);

                if (holder != null) {
                    holder.radioBtnSoundItem.setChecked(true);
                    holder.changeCheckedPosition();
                }
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN) {
                    recyclerView.getViewTreeObserver().removeOnGlobalLayoutListener(this);
                }
            }
        });
    }
```



{% code title="SoundAdapter.java" %}
```java
public void changeCheckedPosition(){
    if (checkedPosition != getAdapterPosition()) {
        notifyItemChanged(checkedPosition);
        checkedPosition = getAdapterPosition();
    }
}
```
{% endcode %}


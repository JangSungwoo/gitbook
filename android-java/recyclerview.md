---
description: '#부스트코스'
---

# RecyclerView

### build.gradle 참조 

```text
dependencies {
    ...
    implementation 'androidx.recyclerview:recyclerview:1.1.0-beta03'
}
```

### 레이아웃 사용 

{% code title="" %}
```markup
<androidx.recyclerview.widget.RecyclerView
    android:id="@+id/recycler_view_sound"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingHorizontal="24dp"
    android:paddingVertical="16dp" />
```
{% endcode %}

### RecyclerView 사용

1\) setLayoutManager 로 레이아웃 형태를 지정한다. 

2\) Adapter를 선언하고 아이템을 추가한다. 

3\) recyclerView 에 setAdapter로 어댑터를 설정한다. 

4\) adapter의 setOnItemClickListener를 사용하여 각 아이템의 클릭이벤트를 처리한다. 

{% code title="MainActivity.java" %}
```java
RecyclerView recyclerView = findViewById(R.id.recycler_view_sound);

LinearLayoutManager linearLayoutManager = new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false);
recyclerView.setLayoutManager(linearLayoutManager);

soundAdater = new SoundAdapter(getApplicationContext());
soundAdater.addItem(new SoundItem("hello1"));
soundAdater.addItem(new SoundItem("hello2"));
soundAdater.addItem(new SoundItem("hello3"));
soundAdater.addItem(new SoundItem("hello4"));
soundAdater.addItem(new SoundItem("hello5"));

recyclerView.setAdapter(soundAdater);

soundAdater.setOnItemClickListener(new SoundAdapter.OnItemClickListener() {
    @Override
    public void onItemClick(RecyclerView.ViewHolder holder, View view, int position) {
        SoundItem item = soundAdater.getItem(position);
        Toast.makeText(getApplicationContext(), "아이템 클릭 : " + item.title, Toast.LENGTH_LONG).show();
    }
});
```
{% endcode %}

### 아이템 정의 

{% code title="SoundItem.java" %}
```java
public class SoundItem {
    String title;

    public SoundItem(String title) {
        this.title = title;
    }
}
```
{% endcode %}

### Adapter 구현 

* onCreateViewHolder : 각 아이템을 위한 xml 레이아웃을 이용해 뷰 객체 생성 후 반환 
* onBindViewHolder : 각 아이템의 데이터를 설정 \(예제에서 ViewHolder의 setItem을 통해\) 

RecyclerView는 Adapter를 ViewHolder 패턴을 사용하여 각각의 뷰를 뷰 홀더에 담아둔다. 

{% code title="SoundAdapter.java" %}
```java
public class SoundAdapter extends RecyclerView.Adapter<RecyclerView.ViewHolder> {
    Context context;
    ArrayList<SoundItem> items = new ArrayList<>();
    OnItemClickListener listener;

    public interface OnItemClickListener {
        void onItemClick(RecyclerView.ViewHolder holder, View view, int position);
    }

    public SoundAdapter(Context context) {
        this.context = context;
    }

    @NonNull
    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        LayoutInflater inflater;
        View itemView;
                inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
                itemView = inflater.inflate(R.layout.recyclerview_item_alarm_sound, parent, false);
                return new ViewHolder(itemView);
    }

    @Override
    public void onBindViewHolder(@NonNull RecyclerView.ViewHolder viewHolder, int position) {
        SoundItem item = items.get(position);
        if (viewHolder instanceof ViewHolder) {
            ((ViewHolder) viewHolder).setItem(item);
            ((ViewHolder) viewHolder).setOnItemClickListener(listener);
        }

    }

    @Override
    public int getItemViewType(int position) {
        return super.getItemViewType(position);
    }

    @Override
    public int getItemCount() {
        return items.size();
    }

    public void setOnItemClickListener(OnItemClickListener listener) {
        this.listener = listener;
    }

    public void addItem(SoundItem item) {
        items.add(item);
    }

    public SoundItem getItem(int position) {
        return items.get(position);
    }

    class ViewHolder extends RecyclerView.ViewHolder {
        TextView txtSound;
        OnItemClickListener listener;

        public ViewHolder(View itemView) {
            super(itemView);
            txtSound = itemView.findViewById(R.id.txt_sound);

            txtSound.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    int position = getAdapterPosition();
                    if (listener != null) {
                        listener.onItemClick(ViewHolder.this, v, position);
                    }
                }
            });
        }

        public void setItem(SoundItem data) {
            txtSound.setText(data.title);
        }

        public void setOnItemClickListener(OnItemClickListener listener) {
            this.listener = listener;
        }

    }
}
```
{% endcode %}

{% hint style="info" %}
Item 의 레이아웃 형태가 다른경우에는 새로운 ViewHolder를 생성하고  

onCreateViewHolder, onBindViewHolder 에서 따로 처리를 해줄 수 있다. 
{% endhint %}

{% embed url="https://academy.realm.io/kr/posts/gotocph-israel-ferrer-camacho-android-ui/" %}

{% embed url="https://academy.realm.io/kr/posts/android-recycler-view/" %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/20492/" %}




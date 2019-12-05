# RecyclerView에서 RadioButton Single choice

ViewHolder 클래스 안에서  RadioButton 의 setOnClickListener 등록시 현재 선택한 RadioButton을 저장한다. 

{% code title="SoundAdapter.java" %}
```java
if (checkedPosition != getAdapterPosition()) {
   notifyItemChanged(checkedPosition);
   checkedPosition = getAdapterPosition();
}
```
{% endcode %}

{% hint style="info" %}
notifyItemChanged 란? 

payload란?
{% endhint %}

`ViewHolder`클래스 내부에서 bind 메소드를 구현한다. 

{% code title="SoundAdapter.java" %}
```java
public void bind(final SoundItem item) {
            if (checkedPosition == -1) {
                radioBtnSoundItem.setChecked(false);
            } else {
                if (checkedPosition == getAdapterPosition()) {
                    radioBtnSoundItem.setChecked(true);
                } else {
                    radioBtnSoundItem.setChecked(false);
                }
            }
        }
```
{% endcode %}

`onBindViewHolder` 메소드에서 구현한 bind 메소드를 호출한다. 

{% code title="SoundAdapter.java" %}
```java
@Override
    public void onBindViewHolder(@NonNull RecyclerView.ViewHolder viewHolder, int position) {
        SoundItem item = items.get(position);
        if (viewHolder instanceof ViewHolder) {
            ((ViewHolder) viewHolder).bind(items.get(position));
            ((ViewHolder) viewHolder).setItem(item);
            ((ViewHolder) viewHolder).setOnItemClickListener(listener);
        }

    }
```
{% endcode %}

### 전체 소스 코드 

{% code title="SoundAdapter.java" %}
```java
public class SoundAdapter extends RecyclerView.Adapter<RecyclerView.ViewHolder> {
    Context context;
    ArrayList<SoundItem> items = new ArrayList<>();
    OnItemClickListener listener;
    static int checkedPosition = -1;


    public interface OnItemClickListener {
        void onItemClick(RecyclerView.ViewHolder holder, View view, int position);
    }

    public SoundAdapter(Context context) {
        this.context = context;
    }

    @NonNull
    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int position) {
        LayoutInflater inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        View itemView = inflater.inflate(R.layout.recyclerview_item_alarm_sound, parent, false);
        return new ViewHolder(itemView);
    }

    @Override
    public void onBindViewHolder(@NonNull RecyclerView.ViewHolder viewHolder, int position) {
        SoundItem item = items.get(position);
        if (viewHolder instanceof ViewHolder) {
            ((ViewHolder) viewHolder).bind(items.get(position));
            ((ViewHolder) viewHolder).setItem(item);
            ((ViewHolder) viewHolder).setOnItemClickListener(listener);
        }

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

    public void addItems(ArrayList<SoundItem> items) {
        this.items = items;
    }

    public SoundItem getItem(int position) {
        return items.get(position);
    }

    public SoundItem getSelected() {
        if (checkedPosition != -1) {
            return items.get(checkedPosition);
        }
        return null;
    }

    class ViewHolder extends RecyclerView.ViewHolder {

        RadioButton radioBtnSoundItem;
        OnItemClickListener listener;

        public ViewHolder(View itemView) {
            super(itemView);
            radioBtnSoundItem = itemView.findViewById(R.id.radiobtn_sound_item);

            radioBtnSoundItem.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    int position = getAdapterPosition();
                    if (listener != null) {
                        listener.onItemClick(ViewHolder.this, v, position);
                        if (checkedPosition != getAdapterPosition()) {
                            notifyItemChanged(checkedPosition);
                            checkedPosition = getAdapterPosition();
                        }
                    }
                }
            });
        }

        public void bind(final SoundItem item) {
            if (checkedPosition == -1) {
                radioBtnSoundItem.setChecked(false);
            } else {
                if (checkedPosition == getAdapterPosition()) {
                    radioBtnSoundItem.setChecked(true);
                } else {
                    radioBtnSoundItem.setChecked(false);
                }
            }
        }

        public void setItem(SoundItem data) {
            radioBtnSoundItem.setText(data.name);
        }

        public void setOnItemClickListener(OnItemClickListener listener) {
            this.listener = listener;
        }
    }
}

```
{% endcode %}

{% embed url="https://medium.com/@droidbyme/android-recyclerview-with-single-and-multiple-selection-5d50c0c4c739" %}


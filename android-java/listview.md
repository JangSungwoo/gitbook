---
description: '#부스트코스'
---

# ListView

## 1\) 아이템을 위한 XML 레이아웃을 정의

{% code-tabs %}
{% code-tabs-item title="item\_view.xml" %}
```markup

```
{% endcode-tabs-item %}
{% endcode-tabs %}

* 
## 

## 2\) 아이템을 위한 뷰 정의



{% code-tabs %}
{% code-tabs-item title="SingerItem.java" %}
```java
public class SingerItem {
    String name;
    String mobile;

    public SingerItem(String name, String mobile){
        this.name = name;
        this.mobile = mobile;
    }
    public String getName(){
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setMobile(String mobile) {
        this.mobile = mobile;
    }

    @Override
    public String toString() {
        return "SingerItem{" +
                "name='" + name + '\'' +
                ", mobile='" + mobile + '\'' +
                '}';
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 3\) 어댑터 정의

```java
 class SingerAdapter extends BaseAdapter{
        ArrayList<SingerItem> items = new ArrayList<SingerItem>();

        @Override
        public int getCount() {
            return items.size();
        }

        public void addItem(SingerItem item){
            items.add(item);
        }
        @Override
        public Object getItem(int position) {
            return items.get(position);
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            SingerItemView view = new SingerItemView(getApplicationContext());
            SingerItem item = items.get(position);
            view.setTvName(item.getName());
            view.setTvMobile(item.getMobile());
            return view;
        }
    }
```

## 4\) 리스트뷰 정의






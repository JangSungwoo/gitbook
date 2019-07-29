---
description: '#부스트코스'
---

# Spinner

Spinner도 리스트뷰와 동일하게 adapter를 사용해야한다. 

다음 예제에서는 아이템하나를 하나의 문자열로만 간단하게 사용하므로 ArrayAdapter를 사용하였다.

Spinner를 통해 아이템을 선택하여 아이템의 이름을 텍스트로 나타내는 예제이다. 

```java
public class MainActivity extends AppCompatActivity {

    TextView textView;
    String[] items = {"짜장면","짬뽕","치킨","탕수육","맥주"};
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = (TextView)findViewById(R.id.textView);
        Spinner spinner = (Spinner)findViewById(R.id.spinner);
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(
                this,android.R.layout.simple_spinner_item,items
        );
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        spinner.setAdapter(adapter);

        spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener(){
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
              textView.setText(items[position]);
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {
                textView.setText("선택 : ");
            }
        });
    }
}
```

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17058/" %}




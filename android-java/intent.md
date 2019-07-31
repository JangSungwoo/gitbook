---
description: '#부스트코스'
---

# Intent

### 액션과 데이터를 사용하는 대표적인 예

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC18D;&#xC131;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ACTION_DIAL tel:01012341234</td>
      <td style="text-align:left">&#xC9C0;&#xC815;&#xB41C; &#xC804;&#xD654;&#xBC88;&#xD638;&#xB97C; &#xC774;&#xC6A9;&#xD574;
        &#xC804;&#xD654;&#xAC78;&#xAE30; &#xD654;&#xBA74;&#xC744; &#xBCF4;&#xC5EC;&#xC90C;</td>
    </tr>
    <tr>
      <td style="text-align:left">ACTION_VIEW tel:01012341234</td>
      <td style="text-align:left">
        <p>&#xC9C0;&#xC815;&#xB41C; &#xC804;&#xD654;&#xBC88;&#xD638;&#xB97C; &#xC774;&#xC6A9;&#xD574;
          &#xC804;&#xD654;&#xAC78;&#xAE30; &#xD654;&#xBA74;&#xC744; &#xBCF4;&#xC5EC;&#xC90C;</p>
        <p>URI &#xAC12;&#xC758; &#xC720;&#xD615;&#xC5D0; &#xB530;&#xB77C; VIEW &#xC561;&#xC158;&#xC774;
          &#xB2E4;&#xB978; &#xAE30;&#xB2A5;&#xC744; &#xC218;&#xD589;&#xD568;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ACTION_EDIT content://contacts/people/2</td>
      <td style="text-align:left">&#xC804;&#xD654;&#xBC88;&#xD638; &#xB370;&#xC774;&#xD130;&#xBCA0;&#xC774;&#xC2A4;
        &#xC815;&#xBCF4;&#xC911;&#xC5D0; ID&#xAC12;&#xC774; 2&#xC778; &#xC815;&#xBCF4;&#xB97C;
        &#xD3B8;&#xC9D1;&#xD558;&#xAE30;&#xC704;&#xD55C; &#xD654;&#xBA74;&#xC744;
        &#xBCF4;&#xC5EC;&#xC90C;</td>
    </tr>
    <tr>
      <td style="text-align:left">ACTION_VIEW content://contacts/people</td>
      <td style="text-align:left">&#xC804;&#xD654;&#xBC88;&#xD638;&#xBD80; &#xB370;&#xC774;&#xD130;&#xBCA0;&#xC774;&#xC2A4;
        &#xB0B4;&#xC6A9;&#xC744; &#xBCF4;&#xC5EC;</td>
    </tr>
  </tbody>
</table>### 명시적인텐트와 암시적 인텐트 

인

### 인텐트의 대표적 속성 

* 범주 
* 타입 
* 컴포넌트 
* 부가데이터 

```text
String receiver = etMoblie.getText().toString();
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("tel:"+receiver));
startActivity(intent);
```



```text
Intent intent2 = new Intent();
ComponentName name = new ComponentName("com.example.examintent","com.example.examintent.MenuActivity");
intent2.setComponent(name);
startActivity(intent2);
```




















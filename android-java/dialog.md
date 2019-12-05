# Dialog 테두리 배경 설정

## DialogFramgent를 사용할경우 아래의 두가지 방법이 있다.

### Java 에서만 변경

{% code title="FragmentDialog.java" %}
```java
getDialog().getWindow().setBackgroundDrawable(new ColorDrawable(Color.TRANSPARENT));
```
{% endcode %}

### XML에서 변경 Java에서 적용

{% code title="MainActivity.java" %}
```java
newFragment.setStyle(DialogFragment.STYLE_NO_FRAME, R.styles.MyDialog);
```
{% endcode %}

{% code title="styles.xml" %}
```markup
<style name="MyDialog" parent="@android:style/Theme.Dialog">
        <item name="android:windowBackground">@android:color/transparent</item>
        <item name="android:backgroundDimEnabled">true</item>
</style>
```
{% endcode %}


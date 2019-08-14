# Untitled

다음과 같은 에러 메세지가 발생할 경우 

{% hint style="danger" %}
java.lang.IllegalStateException: This Activity already has an action bar supplied by the window decor. Do not request Window.FEATURE\_SUPPORT\_ACTION\_BAR and set windowActionBar to false in your theme to use a Toolbar instead.
{% endhint %}

기본 액션바가 지정된 상태에서 툴바를 액션바로 사용할 때 발생하는 에러라고 한다. 

그러므로 툴바를 액션바로 사용하기 위해서는 디폴트 액션바를 비활성화 해야한다. 

여러가지 방법이 있지만 가장 간단한 방법으로 

style.xml 파일에 다음 코드를 추가하여 해결을 하는 방법이 있다. 

```text
<item name="windowActionBar">false</item>
<item name="windowNoTitle">true</item>
```

NoActionBar로 설정을 해도 해결이 된다. 

```text
<style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
```

{% embed url="https://hashcode.co.kr/questions/2872/android-%EC%97%90%EC%84%9C-fragment-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-tab-bar-%EB%A5%BC-%EB%A7%8C%EB%93%A4%EC%97%88%EB%8A%94%EB%8D%B0-%EC%98%A4%EB%A5%98%EA%B0%80-%EB%B0%9C%EC%83%9D%ED%95%98%EC%97%AC-%EC%A7%88%EB%AC%B8%EB%93%9C%EB%A6%BD%EB%8B%88%EB%8B%A4" %}




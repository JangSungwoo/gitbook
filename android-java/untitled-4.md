# Localization

TIimepickerDialog 와 DatepickerDialog의 Language를 변경하고 싶을때 다음과 같이 설정을 하면된다.

```text
private void initLocalization() {
    Locale locale = new Locale("en");
    Locale.setDefault(Locale.ENGLISH);
    Configuration config = new Configuration();
    config.locale = locale;

    this.getBaseContext().getResources().updateConfiguration(config, this.getBaseContext().getResources().getDisplayMetrics());
}
```




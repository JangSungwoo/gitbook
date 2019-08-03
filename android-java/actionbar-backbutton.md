# ActionBar Backbutton 표시하는법

다음과 같이 ActionBar에 Backbutton을 표시하기위해서는 `parentActivityName`  속성에 부모액티비티명을 설정해주면된다. 지원버전이 Android 4.1\(API level 16\)보다 낮은경우 &lt;meta-data&gt;를 설정하여야 한다.

```text
<activity android:name=".CommentListActivity"
    android:parentActivityName=".MainActivity">
    <meta-data
        android:name="android.support.PARENT_ACTIVITY"
        android:value=".MainActivity" />
</activity>
```

{% embed url="https://developer.android.com/training/appbar/up-action" %}




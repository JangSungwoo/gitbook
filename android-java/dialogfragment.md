# DialogFragment



```java
public void showDialog() {
        FragmentManager fragmentManager = getSupportFragmentManager();
        RepeatDialogFragment newFragment = new RepeatDialogFragment();
        newFragment.setStyle(RepeatDialogFragment.STYLE_NO_FRAME, 0);
        newFragment.show(fragmentManager, "dialog");
}
```

```java
public class RepeatDialogFragment extends DialogFragment {


    /** The system calls this to get the DialogFragment's layout, regardless
     of whether it's being displayed as a dialog or an embedded fragment. */
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout to use as dialog or embedded fragment
        return inflater.inflate(R.layout.dialog_fragment_repeat, container, false);
    }

    /** The system calls this only when creating the layout in a dialog. */
    @Override
    public Dialog onCreateDialog(Bundle savedInstanceState) {
        // The only reason you might override this method when using onCreateView() is
        // to modify any dialog characteristics. For example, the dialog includes a
        // title by default, but your custom layout might not need it. So here you can
        // remove the dialog title, but you must call the superclass to get the Dialog.
        Dialog dialog = super.onCreateDialog(savedInstanceState);
        dialog.requestWindowFeature(Window.FEATURE_NO_TITLE);
        return dialog;
    }
}
```

## 화면사이즈로 

```text
private void showCaseView() {
        FragmentManager fragmentManager = getSupportFragmentManager();
        ShowcaseViewDialogFragment newFragment = new ShowcaseViewDialogFragment();
        newFragment.setStyle(ShowcaseViewDialogFragment.STYLE_NO_TITLE, R.style.MyFullSizeDialog);
        newFragment.show(fragmentManager, "dialog");
    }
```



```text
<style name="MyFullSizeDialog" parent="Theme.AppCompat.Light.DialogWhenLarge">
    <item name="android:windowBackground">@android:color/transparent</item>
    <item name="android:windowMinWidthMajor">100%</item>
    <item name="android:backgroundDimEnabled">true</item>
</style>
```


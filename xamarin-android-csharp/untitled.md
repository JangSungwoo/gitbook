# Oreo 이상 버전에서 서비스를 사용하는법



{% code-tabs %}
{% code-tabs-item title="AlarmService.cs" %}
```csharp
[Service(Name = "com.companyname.AlarmService", Exported = true)]
public class AlarmService : Service
{
    public override IBinder OnBind(Intent intent)
    {
        return null;
        //throw new NotImplementedException();
    }
    [return: GeneratedEnum]
    public override StartCommandResult OnStartCommand(Intent intent, [GeneratedEnum] StartCommandFlags flags, int startId)
    {
        if ("startforeground".Equals(intent.Action))
        {
            startForegroundService();
        }
        //else
        {
            Intent activity = new Intent(this, typeof(Activity1));
            StartActivity(activity.AddFlags(ActivityFlags.NewTask));
        }

        return StartCommandResult.Sticky;
        //return base.OnStartCommand(intent, flags, startId);
    }
    void startForegroundService()
    {
        if (Build.VERSION.SdkInt >= BuildVersionCodes.O)
        {
            NotificationCompat.Builder builder;
            //if (Build.VERSION.SdkInt >= BuildVersionCodes.O)
            //{
            builder = new NotificationCompat.Builder(this, "channel_id_1");
            //}
            //else
            //{
            //    builder = new NotificationCompat.Builder(this);
            // }
            builder.SetSmallIcon(Resource.Drawable.design_ic_visibility);
            builder.SetContentTitle("Alarm Service");
            //Intent notificationIntent = new Intent(this, typeof(LockScreen));
            ////Intent notificationIntent = new Intent(this, typeof(LockscreenBroadcastReceiver));
            //notificationIntent.SetFlags(ActivityFlags.ClearTop
            //                            | ActivityFlags.SingleTop);
            //PendingIntent pendingIntent = PendingIntent.GetActivity(this, 0, notificationIntent, 0);
            ////PendingIntent pendingIntent = PendingIntent.GetBroadcast(this, 0, notificationIntent, 0);
            //builder.SetContentIntent(pendingIntent);

            NotificationManager manager = (NotificationManager)GetSystemService(Context.NotificationService);
            manager.CreateNotificationChannel(new NotificationChannel("channel_id_1", "Alarm ch Test", NotificationManager.ImportanceLow));

            StartForeground(1, builder.Build());
        }

    }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="AndroidManifest.xml" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" android:versionCode="1" android:versionName="1.0" package="com.companyname">
    <uses-sdk android:minSdkVersion="21" android:targetSdkVersion="27" />
  <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
  <uses-permission android:name="android.permission.WAKE_LOCK" />
  <application android:label="ServiceApp1.Android"></application>
  <service android:name=".AlarmService"
            android:exported="true"
            android:enabled="true"
            />
  <receiver android:name=".Receiver1"
            android:enabled="true"
            android:exported="true">
  </receiver>

</manifest>

```
{% endcode-tabs-item %}
{% endcode-tabs %}



{% code-tabs %}
{% code-tabs-item title="Receiver.cs" %}
```csharp
[BroadcastReceiver(Enabled = true, Exported = true, DirectBootAware = true, Label = ".Receiver1")]
    public class Receiver1 : BroadcastReceiver
    {
        public override void OnReceive(Context context, Intent intent)
        {
            //Toast.MakeText(context, "Received intent!", ToastLength.Short).Show();
            SetService(context);
        }
        Intent service;
        private void SetService(Context context)
        {
                service = new Intent(context, typeof(AlarmService));
                service.SetAction("startforeground");

            if (Build.VERSION.SdkInt >= BuildVersionCodes.O)
            {
                context.StartForegroundService(service);
            }
            else
            {
                context.StartService(service);
            }
        
        }
    }

```
{% endcode-tabs-item %}
{% endcode-tabs %}
















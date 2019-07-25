# Audio 볼륨 제어

알람소리를 제어하고 싶다면

```csharp
AudioManager am = (AudioManager)this.GetSystemService(Context.AudioService);
am.SetStreamVolume(Stream.Alarm, (int)(am.GetStreamVolume(Stream.Alarm) + 1), 0); // up 1
am.SetStreamVolume(Stream.Alarm, (int)(am.GetStreamVolume(Stream.Alarm) - 1), 0); // down 1
```


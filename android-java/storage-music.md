# Storage music 가져오기

```text
public void getAllTracks(Context context) {
        // gets all tracks
        ContentResolver cr = context.getContentResolver();
        String[] projection =
                {
                        MediaStore.Audio.Media.DATA,
                        MediaStore.Audio.Media._ID,
                        MediaStore.Audio.Media.ALBUM_ID,
                        MediaStore.Audio.Media.TITLE,
                        MediaStore.Audio.Media.ARTIST
                };
//        Cursor cursor = cr.query(uri, projection, null, null, null);
        CursorLoader cursorLoader = new CursorLoader(this,uri, projection, null, null, null);
        Cursor cursor = cursorLoader.loadInBackground();
        songsList = new ArrayList<SoundItem>();
        if(cursor != null){
            if (cursor.moveToFirst())
            {
                do
                {
                    songsList.add(new SoundItem(
                            cursor.getString(cursor.getColumnIndex(projection[0])),
                            cursor.getInt(cursor.getColumnIndex(projection[1])),
                            cursor.getInt(cursor.getColumnIndex(projection[2])),
                            cursor.getString(cursor.getColumnIndex(projection[3])),
                            cursor.getString(cursor.getColumnIndex(projection[4])),
                            1
                    ));
                } while (cursor.moveToNext());
            }
        }
    }
```

{% embed url="https://developer.android.com/guide/topics/providers/content-provider-basics?hl=ko" %}




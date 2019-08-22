---
description: '#부스트코스'
---

# Image Download From Web



### 권한 부여 

```markup
<uses-permission android:name="android.permission.INTERNET" />
```

### AsyncTask로 이미지 다운로드하기 

1\) 생성자에서는 전달받은 이미지 주소와 ImageView의 값을 가져온다.

2\) doInBackground 메소드 안에서는 이미지주소를 통해 받은 이미지 데이터를 비트맵 객체로 저장한다.

*  BitmapFactory 클래스의 decodeStream\(\) 메소드로 간단하게 비트맵 객체를 만듦. 

3\) onPostExcute 메소드에서는 메인스레드에서 이미지 뷰에 표시를 하도록 한다. 

{% code-tabs %}
{% code-tabs-item title="ImagLoadTask.java" %}
```java
public class ImageLoadTask extends AsyncTask<Void, Void, Bitmap> {

    private String urlStr;
    private ImageView imageView;
    
    //한번요청했을때 기억했던 정보를 지우는 방법(1) 
    private static HashMap<String, Bitmap> bitmapHashMap = new HashMap<String, Bitmap>();
    public ImageLoadTask(String urlStr, ImageView imageView) {
        this.urlStr = urlStr;
        this.imageView = imageView;
    }

    @Override
    protected void onPreExecute() {
        super.onPreExecute();
    }

    @Override
    protected Bitmap doInBackground(Void... voids) {
        Bitmap bitmap = null;
        try {
            //한번요청했을때 기억했던 정보를 지우는 방법(2) 
            if(bitmapHashMap.containsKey(urlStr)){
                Bitmap oldBitmap = bitmapHashMap.remove(urlStr);
                if(oldBitmap !=null){
                    oldBitmap.recycle();
                    oldBitmap = null;
                }
            }

            URL url = new URL(urlStr);
            bitmap = BitmapFactory.decodeStream(url.openConnection().getInputStream());
            //한번요청했을때 기억했던 정보를 지우는 방법(3) 
            bitmapHashMap.put(urlStr,bitmap);
        } catch (MalformedURLException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return bitmap;
    }

    @Override
    protected void onProgressUpdate(Void... values) {
        super.onProgressUpdate(values);
    }

    @Override
    protected void onPostExecute(Bitmap bitmap) {
        super.onPostExecute(bitmap);

        imageView.setImageBitmap(bitmap);
        imageView.invalidate();
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 이미지 다운로드 사용 

이미지 주소와 ImageView 를 AsyncTask 클래스의 인자로 넘겨주어 설정을 하고 이미지를 띄운다.  

{% code-tabs %}
{% code-tabs-item title="MainActivity.java" %}
```java
ImageLoadTask task = new ImageLoadTask(movieList.result.get(0).image, imgMoviePoster);
task.execute();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 비트맵 객체의 메모리 해제

비트맵 객체는 메모리에 만들어진 후 해제하지 않으면 계속 남아 있는다. 

앱에서 여러 이미지를 로딩하게 되면 메모리 부족 현상이 발생할 수 있으므로 사용하지않는 비트맵 객체는 recycle 메소드를 이용해 즉시 해제시키는 것이 필요하다. \(Garbage Collector 가 메모리를 해제하더라도\)

 다음은 이전 비트맵 객체를 메모리에서 해제한 후 새로 다운로드 하는 방법을 나타낸다. 

1\) HashMap 객체를 만들고 이미지의 주소와 비트맵 객체와 매핑이 되도록 해준다. 

{% code-tabs %}
{% code-tabs-item title="ImagLoadTask.java" %}
```java
private static HashMap<String, Bitmap> bitmapHashMap = new HashMap<String, Bitmap>();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="ImagLoadTask.java" %}
```java
bitmapHashMap.put(urlStr,bitmap);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

2\) 동일한 주소로 요청하는 경우 이전에 만들었던 비트맵 객체를 해제한다. 

{% code-tabs %}
{% code-tabs-item title="ImagLoadTask.java" %}
```java
if(bitmapHashMap.containsKey(urlStr)){
        Bitmap oldBitmap = bitmapHashMap.remove(urlStr);
        if(oldBitmap !=null){
                oldBitmap.recycle();
                oldBitmap = null;
        }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}



{% hint style="info" %}
UniversalImageLoader 와 같은 라이브러리 간단하게 이미지를 다운받을 수 있음 
{% endhint %}

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17094/" %}




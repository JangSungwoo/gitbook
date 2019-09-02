# Glide

## 이미지 cache 저장

```java
Glide.with(this)
        .load(imageUrl)
        .diskCacheStrategy(DiskCacheStrategy.ALL)
        .into(imageView);
```

## 이미지 cache 로부터 가져오기 

```java
Glide.with(this)
        .load(imageUrl)
        .onlyRetrieveFromCache(true)
        .into(imageView);
```

{% embed url="https://bumptech.github.io/glide/doc/caching.html" %}

{% embed url="https://github.com/bumptech/glide/wiki/Configuration" %}




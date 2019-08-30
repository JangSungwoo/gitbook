# SQL JOIN

```text
SELECT al._id, al.time, sl.title
FROM alarm AS al
JOIN song AS sl
ON sl._id = al.songId
```

```text
SELECT al._id, al.time, sl.title
FROM alarm AS al
JOIN song AS sl
WHERE sl._id = al.songId
```




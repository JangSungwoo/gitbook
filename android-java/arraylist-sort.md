# ArrayList sort



```text
Collections.sort(movieModels, new Comparator<MovieModel>() {
    @Override
    public int compare(MovieModel o1, MovieModel o2) {
        if (o1.getId() > o2.getId()){
            return 1;
        }else if(o1.getId() < o2.getId()){
            return -1;
        }else {
            return 0;
        }
    }
});
```


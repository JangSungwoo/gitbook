# 화면 전환 시 객체를 전달하는 방법

## Serialize

## Parcelable

1. 클래스를 하나 생성한다.
2. Parcelable 인터페이스를 참조한다. 
3. 인터페이스에 선언된 함수들을 구현한다. 

```java
public class UserItemParcelable implements Parcelable {

    String userId;
    float ratingNum;
    String comment;

    protected UserItemParcelable(Parcel src) {
        userId = src.readString();
        ratingNum = src.readFloat();
        comment = src.readString();
    }
    public UserItemParcelable(String userId, float ratingNum, String comment){
        this.userId = userId;
        this.ratingNum = ratingNum;
        this.comment = comment;
    }

    public static  final Parcelable.Creator CREATOR = new Parcelable.Creator(){
        public UserItemParcelable createFromParcel(Parcel src){
            return new UserItemParcelable(src);
        }
        public UserItemParcelable[] newArray(int size){
            return new UserItemParcelable[size];
        }
    };

    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeString(userId);
        dest.writeFloat(ratingNum);
        dest.writeString(comment);
    }

    @Override
    public int describeContents() {
        return 0;
    }


}
```

4. 데이터를 전달한다.

```java
Intent intent = new Intent(getApplicationContext(),MainActivity.class);
UserItemParcelable commentdata = new UserItemParcelable("aswf152",ratingBar.getRating(),etComment.getText().toString());
intent.putExtra("commentdata",commentdata);
//intent.putExtra("Comment",etComment.getText().toString());
setResult(RESULT_OK,intent);
finish();
```

5. 데이터를 받는다.

```java
UserItemParcelable commentdata = (UserItemParcelable) intent.getParcelableExtra("commentdata");
```




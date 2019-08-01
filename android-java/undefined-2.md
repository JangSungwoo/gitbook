---
description: '#부스트 코스'
---

# 외부라이브러리를 참조하는 방법

**다음은 외부라이브러리 중 design 라이브러리를 참조하는 방법이다. 원하는 라이브러리가 있다면 같은방식으로 키워드를 검색하여 참조하면 된다.**

1. File -&gt; Project Structure 
2.  Dependencies -&gt; All Dependencies의 ![](../.gitbook/assets/btnplus.JPG)버튼을 클릭하여 Library Dependency를 선택 \(라이브러리 참조 사진 1\)
3.  design을 검색하여 com.android.support:design 을 선택한 후 ok를 클릭\(라이브러리 참조 사진 2\)

![&#xB77C;&#xC774;&#xBE0C;&#xB7EC;&#xB9AC; &#xCC38;&#xC870; &#xC0AC;&#xC9C4;1](../.gitbook/assets/dependencies_library.png)

![&#xB77C;&#xC774;&#xBE0C;&#xB7EC;&#xB9AC; &#xCC38;&#xC870; &#xC0AC;&#xC9C4;2](../.gitbook/assets/addlibrary.JPG)

참조가 정상적으로 되었다면 build.gradle 파일에 다음과 같이 수정되어있을것이다. 

![build.gradle](../.gitbook/assets/image%20%283%29.png)

{% embed url="https://www.edwith.org/boostcourse-android/lecture/17052/" %}


# DependencyService 사용시 NullReferenceException에러

인터페이스를 구현한 클래스의 namespace위에

\[assembly: Xamarin.Forms.Dependency\(typeof\(Service1\)\)\]

이렇게 입력을 해주어야 한다.


# Android-Architecture
- 안드로이드 아키텍쳐 패턴 공부. MVC, MVP, MVVM

## 무엇을 위하여?

무엇을 위하여 안드로이드 개발을 할 때 아키텍쳐 패턴을 사용해야 하는가?

__데이터와 UI는 프로그램을 구성하는데 필수적인 요소이기 때문에, Model-View 간의 의존성이 강해짐.__

-> M-V와의 관계를 어떻게 처리하느냐에 따라서 여러가지 아키텍쳐 패턴이 나옴.

또한 Clean Code, 테스트를 쉽게 하기 위해서 아키텍쳐 패턴을 사용한다.

>  MVC, MVP, VIPER, MVVM, MVI, FLUX, REDUX...
> 여러가지 아키텍처 패턴 중 MVC, MVP, MVVM에 대해 알아보자.

## MVC
![](https://d3l69s690g8302.cloudfront.net/wp-content/uploads/2017/12/23071849/MVC-Pattern.png)
- Model : DB나 저장소에 접근해, 데이터를 수정, 삽입, 삭제, 검색 등을 수행하는 코드
- View : 사용자에게 보여지는 UI (User-Interface)
- Controller : 사용자에게 입력을 받고 처리하는 부분.
- Activity / Fragment : MVC 패턴에서의 View와 Controller의 역할을 함
  - 사용자에게 이벤트를 받는 Controller의 역할, 화면을 보여주는 View의 역할
  - 안드로이드에서의 MVC 패턴은 Activity와 Fragment가 View와 Controller의 역할을 동시에 함.
- 작동 순서
  1. Controller에서 입력을 받고 Model을 업데이트함.
  2. Controller는 업데이트한 Model을 보여줄 View를 선정함.
  3. View는 Model에 따라서 UI를 변경함.

특징 : Controller는 View를 여러 개 선택할 수 있다. (Controller : View = 1 : n)

장점 : 단순하며, 코드가 간결할 경우 이해가 쉬움. Model과 View는 Controller와 독립적이다.

단점 : View와 Model의 의존성이 강하기 때문에 코드가 길어져 유지보수가 힘들어질 수 있다.

-> View와 Model간의 의존성이 강하다는 문제가 발생

## MVP -  [구현](https://github.com/KRMKGOLD/studyMVP)

 - Model, View, Presenter
 - MVC에서의 Model과 View 간 의존성이 없는 아키텍쳐 패턴

![](https://t1.daumcdn.net/cfile/tistory/273A7E4A5844B8B939)

- Model : MVC의 Model과 동일.
- View : MVC의 View와 유사하나, Action을 받는다.
- Presenter : View에서의 Action을 Model을 통해 데이터를 수정하여 다시 View에게 전달하는 View와 Model의 매개체 역할

- 작동 순서
  1. View에서 이벤트를 받고 Presenter에 이벤트를 전달
  2. Presenter가 Model에게 데이터를 요청하고, Model은 데이터를 Presenter에게 보내준다.
  3. Presenter는 View에게 데이터를 보내주고, View는 UI를 갱신한다.

장점 : M-V간의 의존성이 적어 테스트 코드 작성이 쉽고, 확장성이 좋아진다.

단점 : M-V간의 의존성이 낮아진 대신 View-Presenter 의존성이 강함(View : Presenter = 1 : 1) , 클래스의 개수가 많아진다.

-> MVC에서의 Model-View 관계를 MVP에서는 해결했다!

-> View-Presenter간의 의존성이 강하고, 중복 코드가 발생하는 경우가 많음.

## MVVM - [구현](https://github.com/KRMKGOLD/Android_MVVMSample/tree/master)
 - Model, View, ViewModel
 - MVP의 문제를 해결하기 위해서 Presenter를 분리해 보았다! -> MVVM
 - MVC에서의 Model-View간의 의존성과 MVP에서의 View-Presenter간의 의존성도 해결하기 위한 아키텍쳐 패턴

![](https://cdn-images-1.medium.com/max/1600/1*VLhXURHL9rGlxNYe9ydqVg.png)

- Model  : MVC, MVP와 동일
- View : MVC, MVP와 동일
- ViewModel : View를 나타내주기 위한 Model, View의 Presentation Logic를 처리
  - Presentation Logic : 실제 눈에 보이는 GUI 화면을 구성하는 코드.
- 작동 순서

  1. View에서 이벤트를 받고 커맨드 패턴으로 ViewModel에게 이벤트를 전달해준다.
     - Command Pattern : 실행될 기능을 캡슐화함으로써 주어진 여러 기능을 실행할 수 있는 재사용성이 높은 클래스를 설계하는 패턴
  2. ViewModel은 Model에게 데이터를 요청하고, Model은 ViewModel에게 요청받은 데이터를 전달한다.
  3. ViewModel은 Model에게서 받은 데이터를 가공하고 View에게 전달한다
  4. View는 받은 데이터를 Data-Binding하여 UI를 갱신한다.
     - Data-Binding : 공급자와 소비자의 데이터 원본을 함께 바인딩하고 동기화하는 일반적인 기술.
- 커맨드 패턴이나 Data-Binding을 통해서, V-VM간 의존성을 없앨 수 있다.

장점 : View가 Model이나 ViewModel과 의존성 없이 독립적이며, 중복되는 코드들을 모듈화할 수 있다.

단점 : ViewModel의 구현이 어렵다.

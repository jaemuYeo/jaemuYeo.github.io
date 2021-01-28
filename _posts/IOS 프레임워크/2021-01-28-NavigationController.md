---
title: "UIKit) Navigation Controller"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-28

last_modified_at: 2021-01-28
---

이 글의 전반적인 내용은 [KXCoding](https://kxcoding.com/)을 참고하였습니다.

> 글에서 VC는 View Controller의 약자입니다.

# [Navigation Controller](https://developer.apple.com/documentation/uikit/uinavigationcontroller)

## Navigation Controller 개요

네비게이션 컨트롤러는 계층 적 콘텐츠를 탐색하기위한 **스택** 기반 체계를 정의하는 컨테이너뷰 컨트롤러이다.

```swift
class UINavigationController: UIViewController
```

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/70311145/106114991-99999c80-6193-11eb-8705-c6f72563f856.gif)

네비게이션 컨트롤러는 계층구조로 구성된 content를 순차적으로 보여주는 Container View Controller이고,

탐색으로 앱의 Content를 보여주기 적절하다.

그리고 Child View Controller를 하나이상 추가해야한다.

Child 목록은 배열로 관리하며 스택형식으로 구현되어있다. ( Navigation Stack)

<img width="806" alt="스크린샷 2021-01-28 오후 6 24 46" src="https://user-images.githubusercontent.com/70311145/106117206-2180a600-6196-11eb-9e45-b7774979ce79.png">

스택은 화면이 바뀌는 것을 PUSH, POP 형식으로 표현한다.

네비게이션 컨트롤도 뷰 컨트롤러 이기 때문에 Root VC를 가지고 있다.

가장 먼저 추가된 화면은 Root VC이고, 가장 마지막에 추가된 컨트롤러는 TopVC이다.

네비게이션 컨트롤 Root View의 상단에는 Navigation Bar가 항상 표시된다.

하단에는 Tool Bar가 표시되고 사용자가 지정해서 사용할 수 있다.

두 Bar는 커스텀을 할 수 있고 버튼을 통해 VC이동 또는 검색기능도 구현할 수 있다.

두 Bar 사이의 나머지 영역에는 TopVC가 표시된다.

<img width="779" alt="스크린샷 2021-01-29 오전 12 54 21" src="https://user-images.githubusercontent.com/70311145/106163475-8bb43d80-61cc-11eb-8514-094e2f168657.png">

네비게이션 컨트롤러를 임베드 하는 방법은 세가지가 있다.

1. Xcode 툴바에서 Editor - Embed In - Navigation Controller 선택

2. cmd + shift + L 을 눌러 Navigation Controller를 인터페이스빌더에 드래그 배치

<img width="322" alt="스크린샷 2021-01-29 오전 12 58 42" src="https://user-images.githubusercontent.com/70311145/106164345-33317000-61cd-11eb-926c-f34e16ba35c6.png">

3. 임베드 할 VC를 선택 후 하단 우측에서 선택

---

## [Navigation Bar](https://developer.apple.com/documentation/uikit/uinavigationbar)

일반적으로 네비게이션 컨트롤러와 함께 화면 상단의 막대에 표시되는 네비게이션 컨트롤이다.

```swift
class UINavigationBar: UIView
```

<img width="438" alt="스크린샷 2021-01-28 오후 6 33 48" src="https://user-images.githubusercontent.com/70311145/106118400-6eb14780-6197-11eb-8e05-f475a94e76c4.png">

TopVC와 연관된 버튼과 타이틀을 표시한다.

버튼은 Bar의 왼쪽과 오른쪽에 표시되고, 기본적으로 왼쪽에는 이전화면으로 Pop할 수있는 백 버튼이 있다.

버튼은 항상 UIBarButtonItem 인스턴스로 생성해야 한다.

```swift
class UIBarButtonItem : UIBarItem
```

일반적인 다른 뷰를 표현할 때에도 항상 UIBarButtonItem으로 랩핑하여 추가해야한다.

IOS11부터 Large Title 모드가 생겼다. 이 모드를 설정하게되면 바 버튼 밑에 타이틀이 크게 구현된다.

---

## 화면 전환 구현 (Push & Pop)

루트뷰로 연결된 VC에는 네비게이션 아이템을 설정할 수 있는 옵션이 표시된다.

네비게이션을 통한 액션 세그는 show 방식으로 전달한다.

<img width="503" alt="스크린샷 2021-01-29 오전 1 13 23" src="https://user-images.githubusercontent.com/70311145/106166278-54935b80-61cf-11eb-8039-ac4772fcf0ac.png">

연결 후에는 연결한 씬에 화살표가 표시되고 네비게이션 바가 추가된걸 볼 수 있다.

루트 뷰 컨트롤러와 달리 왼쪽에 Back 버튼이 표시된다.

네비게이션 스택에 저장되는 컨트롤러 중에서 루트뷰 컨트롤러를 제외한 나머지 뷰컨트롤러들은

Back 버튼이 자동으로 표시된다. (이전 화면으로 Pop 하는 버튼)

<img width="628" alt="스크린샷 2021-01-29 오전 1 14 09" src="https://user-images.githubusercontent.com/70311145/106166283-56f5b580-61cf-11eb-9007-eb63f336948d.png">

![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/70311145/106167284-6295ac00-61d0-11eb-95f8-a16ea21d6e04.gif)

세그 버튼을 누르면 화면이 Push되고 Back 버튼을 누르면 화면이 Pop되는 것을 볼 수있다.

화면전환을 코드로 구현하게 될때에는 네비게이션 바에 Back버튼을 생성하는 것과

이전화면으로 돌아가는 기능은 네비게이션 컨트롤러가 담당하지만

navigation VC와 child VC 인스턴스를 생성하는 코드는 직접구현해야하고,

새로운 child를 표시하는 코드도 직접 구현해야한다.

child를 생성할 때에는 각 VC에 입력된 storyboard ID를 활용한다.

이번에는 화면을 더 추가하고 코드로 구현해 보자!

<img width="846" alt="스크린샷 2021-01-29 오전 1 58 26" src="https://user-images.githubusercontent.com/70311145/106172024-a0e19a00-61d5-11eb-87d0-ceff4de02d37.png">

각 화면에 컨트롤러 파일을 만들어주고 storyboard ID를 입력해준다.

<img width="536" alt="스크린샷 2021-01-29 오전 1 30 03" src="https://user-images.githubusercontent.com/70311145/106168353-85749000-61d1-11eb-8fd2-5c4111358e9d.png">

<img width="868" alt="스크린샷 2021-01-29 오전 1 50 16" src="https://user-images.githubusercontent.com/70311145/106170956-5b709d00-61d4-11eb-941e-825c081c1d23.png">

child인스턴스를 생성후 storyboard ID를 입력하고

네비게이션 컨트롤러에 접근해서 Push방식을 구현한 것이다.

Pop방식은 Back버튼이 구현하지만 네비게이션바를 커스텀해서 버튼이 생성되어있지 않을 때

코드를 통해 구현할 수 있다.

<img width="520" alt="스크린샷 2021-01-29 오전 1 55 37" src="https://user-images.githubusercontent.com/70311145/106171623-19942680-61d5-11eb-805d-9ac2d4abf499.png">

위 코드를 입력하면 네비게이션 스택에서 제거 후 이전화면으로 돌아간다.

![ezgif com-gif-maker (3)](https://user-images.githubusercontent.com/70311145/106172318-0897e500-61d6-11eb-81e9-5e909da9e272.gif)

세그웨이를 이용해서 첫번째 화면이나 지정된 화면으로 돌아가고 싶다면 **Unwind Segue**를 사용해야 한다.

Unwind Segue를 사용할 때에는 돌아갈 VC 클래스에 Unwind segue와 연결할 액션 메서드를 추가해야 한다.

<img width="731" alt="스크린샷 2021-01-29 오전 2 12 01" src="https://user-images.githubusercontent.com/70311145/106173560-6a0c8380-61d7-11eb-9db2-fbe0465e0d69.png">

그러고나서 Push를 할 VC로 돌아가 Exit 쪽으로 해당 버튼을 드래그해주면

방금 추가했던 unwind 메서드에 연결할 수 있다.

<img width="394" alt="스크린샷 2021-01-29 오전 2 14 20" src="https://user-images.githubusercontent.com/70311145/106173849-bb1c7780-61d7-11eb-8d46-589c7250a69f.png">

코드를 통해 원하는 VC로 푸시하는 것을 구현한다면 방금처럼

클래스에 Unwind 메서드를 구현해줄 필요는 없다.

네비게이션 컨트롤러에 접근해 popToRootViewController 메서드를 true로 해주면 된다.

<img width="540" alt="스크린샷 2021-01-29 오전 2 25 11" src="https://user-images.githubusercontent.com/70311145/106175244-3af71180-61d9-11eb-8cbd-99997e8ac46a.png">

루트뷰가 아닌 원하는 VC로 이동하고 싶다면 Unwind Segue 방식을 사용하거나 코드로 구현가능하다.

네비게이션 컨트로러는 네비게이션 스택에 추가되있는 child를 배열로 저장한다.

이 배열에 접근할 때에는 viewController속성을 사용한다.

이동할 뷰의 인스턴스를 찾아서 상수에 바인딩 후 popToViewController의 파라미터에 전달하면 된다.

<img width="962" alt="스크린샷 2021-01-29 오전 2 29 32" src="https://user-images.githubusercontent.com/70311145/106175761-d6888200-61d9-11eb-9dda-0dd2d0856401.png">

![ezgif com-gif-maker (4)](https://user-images.githubusercontent.com/70311145/106175962-0fc0f200-61da-11eb-84af-6b2fefe3a29c.gif)

---

### Navigation Item & NavigationBar

네비게이션바는 네비게이션 스택이 업데이트 될 때 마다 함께 업데이트 된다.

표시할 버튼과 타이틀은 Child VC에서 개별적으로 저장한다.

네비게이션 아이템에 원하는 항목을 저장해두면 Top VC로 지정되었을 때 네비게이션바에 표시된다.

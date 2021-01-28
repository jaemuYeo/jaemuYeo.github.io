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

# [Navigation Controller](https://developer.apple.com/documentation/uikit/uinavigationcontroller)

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

스택은 화면이 바뀌는 것을을 PUSH, POP 형식으로 표현한다.

네비게이션 컨트롤도 뷰 컨트롤러 이기 때문에 Root VC를 가지고 있다.

가장 먼저 추가된 화면은 Root VC이고, 가장 마지막에 추가된 컨트롤러는 TopVC이다.

네비게이션 컨트롤 Root View의 상단에는 Navigation Bar가 항상 표시된다.

하단에는 Tool Bar가 표시되고 사용자가 지정해서 사용할 수 있다.

두 Bar는 커스텀을 할 수 있고 버튼을 통해 VC이동 또는 검색기능도 구현할 수 있다.

두 Bar 사이의 나머지 영역에는 TopVC가 표시된다.

---

## Navigation Bar

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

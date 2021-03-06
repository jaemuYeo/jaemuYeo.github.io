---
title: "UIKit) Navigation Controller"

excerpt: " navigation controller & tab bar controller"

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

3. 임베드 할 VC를 선택 후 하단 우측에서 선택

<img width="322" alt="스크린샷 2021-01-29 오전 12 58 42" src="https://user-images.githubusercontent.com/70311145/106164345-33317000-61cd-11eb-926c-f34e16ba35c6.png">

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

### Navigation Item & NavigationBar

네비게이션바는 네비게이션 스택이 업데이트 될 때 마다 함께 업데이트 된다.

표시할 버튼과 타이틀은 Child VC에서 개별적으로 저장한다.

네비게이션 아이템에 원하는 항목을 저장해두면 Top VC로 지정되었을 때 네비게이션바에 표시된다.

<img width="262" alt="스크린샷 2021-01-29 오전 3 44 45" src="https://user-images.githubusercontent.com/70311145/106184026-5ae00280-61e4-11eb-92ab-65c7de1aa892.png">

네비게이션컨트롤러에서 네비게이션바를 선택 후 속성을 보면 위 사진처럼 구성되어있다.

스타일을 정할 수 있고 배경을 투명하게 하거나 타이틀을 라지사이즈로 바꿀 수 있다.

Back버튼의 이미지를 지정할 수 있고 타이틀의 두 스타일에 따라 폰트와 사이즈, 컬러 등을 지정할 수 있다.

### Title 설정

인터페이스 빌더

<img width="694" alt="스크린샷 2021-01-29 오전 3 35 54" src="https://user-images.githubusercontent.com/70311145/106183501-9e863c80-61e3-11eb-8871-1d87484c36d9.png">

코드

<img width="412" alt="스크린샷 2021-01-29 오전 3 39 05" src="https://user-images.githubusercontent.com/70311145/106183513-a1812d00-61e3-11eb-966a-347340b09db9.png">

### Bar Button Item

<img width="642" alt="스크린샷 2021-01-29 오전 3 50 05" src="https://user-images.githubusercontent.com/70311145/106184582-16089b80-61e5-11eb-8cc9-217df50c38c1.png">

System Item이 Custom으로 되어있으면 버튼의 타이틀이나 이미지 등을 직접 설정한다.

System Item에는 직관적인 고유의 이미지들이 여러개 있다.

코드를 통해 bar button item에 접근하려면 Target-Action 메커니즘을 사용한다.

네비게이션바에 추가되는 뷰는 항상 bar button item에 임베드되어서 추가된다.

<img width="253" alt="스크린샷 2021-01-29 오전 4 00 28" src="https://user-images.githubusercontent.com/70311145/106185729-8a900a00-61e6-11eb-93f6-36b8ba0e687c.png">

스토리보드를 통해 추가하면 자동으로 추가되지만 코드를 통해 추가하면 직접 임베드 해야한다.

<img width="983" alt="스크린샷 2021-01-29 오전 4 10 47" src="https://user-images.githubusercontent.com/70311145/106186891-3ede6000-61e8-11eb-99ba-1b16af2d7dcf.png">

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/106186869-384fe880-61e8-11eb-9382-29cfba80ac22.gif)

### Back Button

네비게이션에 연결된 뷰 중에 루트뷰가 아니라면 이전화면으로 돌아가는

Back Button이 자동으로 생성된다.

Back Button의 타이틀은 기본적으로 이전화면의 타이틀로 설정된다.

하지만 타이틀을 넣을 공간이 부족하다면 Back 문자로 전환된다.

Back Button을 직접 추가한 버튼과 함꼐 사용하고 싶다면 navigation item의

속성에서 Left Items Supplement를 체크하거나 코드로 구현해주면 된다.

<img width="638" alt="스크린샷 2021-01-29 오전 4 25 22" src="https://user-images.githubusercontent.com/70311145/106188226-09d30d00-61ea-11eb-9a7b-57b2f35afa08.png">

<img width="475" alt="스크린샷 2021-01-29 오전 4 27 53" src="https://user-images.githubusercontent.com/70311145/106188488-5dddf180-61ea-11eb-92e1-4616cd6d495c.png">

---

### [ToolBar](https://developer.apple.com/documentation/uikit/uitoolbar)

툴 바는 인터페이스의 하단에 위치해 있고 하나이상의 버튼을 표시하는 컨트롤이다.

네비게이션 컨트롤의 속성에서 Shows Toolbar를 체크해도 되고,

라이브러리 창을 열어 툴 바를 드래그해서 화면에 배치시켜도 된다.

네비게이션과 마찬가지로 트렌지션이 발생할 때 마다 자동으로 업데이트 된다.

<img width="265" alt="스크린샷 2021-01-30 오전 1 00 13" src="https://user-images.githubusercontent.com/70311145/106297928-9b985400-6296-11eb-96fc-397fca47556e.png">

툴 바에서 생성한 BarButtonItem은 왼쪽에서부터 정렬된다.

<img width="269" alt="스크린샷 2021-01-30 오전 1 03 48" src="https://user-images.githubusercontent.com/70311145/106298276-0cd80700-6297-11eb-9763-89d9e4997c4d.png">

Fixed Space는 작은 간격을 정렬할 떄 사용하고

Flexible Space는 비어있는 툴바에 크게 간격을 정렬할 때 사용한다.

<img width="981" alt="스크린샷 2021-01-30 오전 1 16 09" src="https://user-images.githubusercontent.com/70311145/106299640-bf5c9980-6298-11eb-9b71-3fcd6ea6c799.png">

코드로 Toolbar를 구현할 때에는 해당하는 BarButtonItem을 생성 후

setToolbarItems 메서드에서 배열안에다가 넣어주면 된다.

<img width="482" alt="스크린샷 2021-01-30 오전 1 14 44" src="https://user-images.githubusercontent.com/70311145/106299509-950adc00-6298-11eb-8bb5-6f57d5680f77.png">

---

## [Tab Bar Controller](https://developer.apple.com/documentation/uikit/uitabbarcontroller)

```swift
class UITabBarController: UIViewController
```

childVC를 배열로 관리하는 컨테이너 뷰 컨트롤러이다.

다중 선택 인터페이스를 관리하는 컨테이너 뷰 컨트롤러로, 선택 항목에 따라 표시 할 childVC가 결정된다.

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/106300716-2b8bcd00-629a-11eb-9dce-89662e50bb58.gif)

탭바컨트롤러의 루트뷰에는 두개가 표시된다.

아랫쪽에는 탭바가 표시되고, Child 수 만큼 탭 바 아이템이 추가된다.

원하는 아이템을 선택하면 나머지 공간에 해당 Child가 표시된다.

탭바 컨트롤러에서 아이템의 갯수가 제한된다.

portrait 모드에서는 다섯개로 제한되고, 최대 갯수가 초과되면 More Item으로 표시된다.

More Item을 선택하게되면 나머지 아이템이 표시되어있는 More Navigation Controller가 표시된다.

<img width="460" alt="스크린샷 2021-01-30 오후 4 46 59" src="https://user-images.githubusercontent.com/70311145/106350834-44889280-631b-11eb-8779-7366d9297eb9.png">

모든 child는 연관된 Tab bar Item을 가지고 있다. 타이틀과 이미지를 저장하면 탭바에 표시된다.

뱃지 문자열을 설정하면 아이탬의 이미지 오른쪽 상단에 표시된다.

Portrait모드에서는 이미지 아랫쪽에 타이틀이 표시된다. 이러한 탭바를 Regular Tab Bar라고한다.

LandScape 모드에서는 이미자와 타이틀이 나란히 표시되고, Compact Tab Bar라고 한다.

---

### Tab Bar Controller 사용해보기

<img width="542" alt="스크린샷 2021-01-30 오후 8 06 37" src="https://user-images.githubusercontent.com/70311145/106354644-adc9cf00-6336-11eb-9910-b8dd6da1b091.png">

네비게이션 컨트롤러와 같은 방식으로 임베드하면 된다.

최초에는 하나의 아이템이 생성되어있다.

<img width="263" alt="스크린샷 2021-01-30 오후 8 07 32" src="https://user-images.githubusercontent.com/70311145/106354662-ce922480-6336-11eb-8a5e-eb3929688c21.png">

아이템의 속성은 기본적으로 System Item이 커스텀으로 되어있고 여러가지 기본 옵션들을

사용할 수 있다. 커스텀이 아닌 다른 속성이 선택되어 있는 상태에서 Bar Item의

타이틀이나 이미지를 변경하게되면 다시 System Item이 커스텀으로 설정된다.

연결을 할 때는 세그를 연결하든 해당 뷰로 컨트롤을 누른상태에서 드래그한 후

view controllers를 통해 연결하면 되고, 지금은 네개이 child를 가지고있고

그러므로 네개의 bar button item이 생성된 것을 볼 수 있다.

<img width="175" alt="스크린샷 2021-01-30 오후 8 10 23" src="https://user-images.githubusercontent.com/70311145/106354715-33e61580-6337-11eb-9d1f-8185c4d75b18.png">

<img width="684" alt="스크린샷 2021-01-30 오후 8 11 22" src="https://user-images.githubusercontent.com/70311145/106354737-55df9800-6337-11eb-9e74-26847133db5a.png">

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/106354855-f2a23580-6337-11eb-8850-494eefb9e3b4.gif)

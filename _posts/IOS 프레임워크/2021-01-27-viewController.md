---
title: "UIKit) View Controller & Life Cycle"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-27

last_modified_at: 2021-01-27
---

이 글의 전반적인 내용은 [KXCoding](https://kxcoding.com/)을 참고하였습니다.

# [View Controller](https://developer.apple.com/documentation/uikit/uiviewcontroller)

뷰 컨트롤러는 UIViewController클래스로 구현되어있다.

보통은 이 클래스를 그대로 사용하지 않고 서브클래싱하여 필요한 기능을 추가한다.

스토리보드에서 아웃렛과 액션을 연결하기 위해서 이 클래스를 상속한 새 클래스를 만들고

연결할 컨트롤이 포함되어있는 씬에 커스텀 클래스로 설정해야한다.

화면 표시 시점에 따라 이벤트를 처리할 때에도 서브클래싱이 필요하다.

뷰 컨트롤러 생명주기(Life Cycle)가 대표적인 예이다.

기능을 제공하는 메서드와 이벤트가 발생할 때마다 뷰 컨트롤러가 직접 호출하는 콜백 메서드가 함꼐 제공되어

필요에 맞게 사용해야한다.

---

### 뷰 컨트롤러의 역할

화면에 표시되는 뷰를 관리한다. 뷰컨트롤러는 하나의 루트뷰를 가지고 있다.

**루트 뷰**는 UI를 표시할 프레임을 제공하고, 뷰 계층을 관리한다.

<img width="388" alt="스크린샷 2021-01-27 오후 3 07 17" src="https://user-images.githubusercontent.com/70311145/105950229-5e26a180-60b1-11eb-8301-a8e320e63a55.png">

루트 뷰에 접근할 때는 View속성을 사용하고 루트뷰에 속한 나머지 뷰에 접근할 때에는

Outlet 또는 View Tagging을 사용한다.

뷰 컨트롤러는 뷰에서 발생하는 이벤트를 처리해준다.

컨트롤러가 이벤트를 직접 처리할 수 있지만 Target-Action 메커니즘 or 델리게이트패턴을 활용하여 이벤트를 처리한다.

노티피케이션을 통해 다양한 시스템 이벤트를 처리하는 것도 주로 뷰 컨트롤러에서 구현한다.

마지막으로 뷰 컨트롤러는 화면전을 한다. 코코아 터치 프레임워크는 화면 전환에 필요한

필요한 모든 기능을 제공한다.

<img width="351" alt="스크린샷 2021-01-27 오후 3 19 16" src="https://user-images.githubusercontent.com/70311145/105951220-0a1cbc80-60b3-11eb-8c18-92ba609fea9a.png">

모든 앱에는 윈도우를 가지고 있다. 윈도우는 UI를 출력할 프레임을 정의하고 실제로 UI를 출력하는 것은

뷰 컨트롤러이다. 앱 시작 시점에 새로운 뷰 컨트롤러를 생성하고, 윈도우에 루트 뷰 컨트롤러고 지정해야한다.

스토리보드 개발시 자동으로 생산이 되지만 코드베이스로 구현시 하나하나 직접 구현해주어야한다.

뷰 컨트롤러는 두가지 종류가 있다.

<img width="682" alt="스크린샷 2021-01-27 오후 3 27 28" src="https://user-images.githubusercontent.com/70311145/105951953-3258eb00-60b4-11eb-82b4-64a771823d63.png">

- Content View Controller - 화면에 표시할 UI를 구성

- Container View Controller - 하나 이상의 Child View Controller를 관리 (배치, 화면전환)

---

## 뷰 컨트롤러 생명주기(Life Cycle)

<img width="716" alt="스크린샷 2021-01-27 오후 4 55 49" src="https://user-images.githubusercontent.com/70311145/105965782-2e829400-60c7-11eb-991c-9fdaa9406d9d.png">

뷰 컨트롤러는 스토리보드나 코드를 통해 생성되고 루트뷰가 화면에 표시되어있는 동안에는

계속 유지된다. 루트뷰가 화면에서 사라지고 뷰 컨트롤러의 참조 카운트가 0이 되면 메모리에서 제거된다.

<img width="421" alt="스크린샷 2021-01-27 오후 5 52 21" src="https://user-images.githubusercontent.com/70311145/105966789-735afa80-60c8-11eb-9a5e-2ef5b47e7fec.png">

생성 시점에 init()이 호출되고 메모리에서 제거되기 전에 deinit()이 호출된다.

뷰 컨트롤러가 메모리에서 유지되는 동안에는 루트뷰의 가시성에 따라 이벤트가 발생 한다.

viewDidLoad - 루트뷰가 메모리에 생성되면 호출 ( 뷰가 로드 되었다 )

viewWillAppear - 루트뷰가 추가되기 직전에 호출 ( 뷰가 나타날 것이다 )

viewDidAppear - 루트뷰가 뷰 계층에 추가되었을 때 호출 (뷰가 나타났다 )

viewWillDisappear - 루트뷰가 뷰 계층에서 제거되기 진전에 호출 (뷰가 사라질 것이다 )

viewDidDisappear - 루트뷰가 뷰 계층에서 제거되었을 때 호출 (뷰가 사라졌다 )

---

## 뷰 계층 구조

view의 계층 구조는 superView, subView, siblingView로 특정되며 이는 drawing 순서를 결정 짓는다.

superView와 subView의 관계에서는 superView가 우선해서 그려진다.

동일한 superView 내부에 여러 siblingView가 있다면 먼저 addSubview가 된 순으로

그려진다. 두 sibilingView가 겹쳐 있다면 먼저 drawing된 View가 가려진다.

<img width="696" alt="스크린샷 2021-01-27 오후 6 59 56" src="https://user-images.githubusercontent.com/70311145/105975054-e026c280-60d1-11eb-8af7-a615b9714327.png">

**SuperView와 SubView의 계층구조에 따른 특징**

- superView를 제거하면 subView도 함께 제거된다
- superView의 투명도는 subView에도 적용된다
- superView의 size가 변하면 subView의 size도 함께 변한다
- superView는 subViews를 array로 관리한다

addSubView(\_:)로 subView를 추가하고 removeFromSuperView()를 통해 제거할 수 있다.

이 외에도 subView 표시 순서를 바꾸거나 위치를 교체하는 등 여러 메서드가 구현되어있다.

---

## Container View Controller

위에 있던 글처럼 Content View는 화면에 표시할 UI를 구성하고 관련된 이벤트를 처리한다.

반면 **Container View Controller**는 하나 이상의 Child View Controller를 관리하고

Layout과 Transition을 관리한다. 그리고 UI구성과 이벤트 처리는 Child View Controller가 담당한다.

Container View Controller는 코코아 터치 프레임워크를 통해 기본적으로 제공하고

가장 대표적인 Container View Controller는 **Navigation Controller**가 있다.

Navigation Controller는 Child View Controller를 Push & Pop 방식으로 전환한다.

Custom Container View Controller는 UIViewController가 제공하는 API를 활용해서

자유롭게 구현할 수 있다.

Container View Controller를 통해 표시하면 구현이 단순해지고 유지보수가 쉬워지는 장점이 있다.

---
title: "ios) Margins & Guides + (Adaptive Layout)"

categories:
  - AutoLayout

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-14

last_modified_at: 2021-02-14
---

# Layout Margins & Guides

## [Layout Margin](https://developer.apple.com/documentation/uikit/uiview/1622566-layoutmargins)

<img width="507" alt="스크린샷 2021-02-19 오후 4 03 20" src="https://user-images.githubusercontent.com/70311145/108469651-00f6c800-72cc-11eb-8324-9dcf7949c6b1.png">

Layout Margin은 뷰에 표시되는 내용과 뷰의 Bound 사이의 간격을 말한다.

ios8이 출시하면서 도입이 되었다.

UIView 클래스에 속성으로 선언되어있고, Top, Bottom, Left, Right의 마진을 개별적으로 지정한다.

<img width="491" alt="스크린샷 2021-02-19 오후 6 10 24" src="https://user-images.githubusercontent.com/70311145/108483183-c1d17280-72dd-11eb-8386-43b0fcd45168.png">

ios11버젼이 나오면서 safeArea가 도입되었고, 이전 버젼과의 다른 방식으로 동작하며

ios11에서는 safeArea나 다른 속성의 영향을 받을 수 있기 때문에 차이점을 잘 비교해야한다.

현재 오렌지뷰는 루트뷰와의 Top, Bottom, Left, Right 제약이 걸려있다.

<img width="546" alt="스크린샷 2021-02-19 오후 6 37 32" src="https://user-images.githubusercontent.com/70311145/108486572-8f297900-72e1-11eb-8f72-cc9c67e1e560.png">

루트뷰를 선택후 사이즈 인스펙터를 보면 Layout Margins에는 기본값이 Default로 되어있다.

<img width="261" alt="스크린샷 2021-02-19 오후 6 38 08" src="https://user-images.githubusercontent.com/70311145/108486774-cd269d00-72e1-11eb-8b88-0b209d1c47f4.png">

Layout Margins을 Fixed로 바꾸고 네가지 방향에 100씩 지정하면 오렌지뷰가

루트뷰로부터 각각 100의 margin을 가지게 되는 것을 확인할 수 있다.

<img width="574" alt="스크린샷 2021-02-19 오후 6 38 37" src="https://user-images.githubusercontent.com/70311145/108486779-cef06080-72e1-11eb-8f09-12383d3ff05d.png">

ios11부터 루트뷰의 Layout Margin이 Safe Area를 고려한다.

네비게이션 바 or 탭 바가 추가되어있다면 각각에 겹치지 않는 최소 Margin이 지정된다.

다시한번 루트 뷰의 사이즈 인스펙터를 보면 \*\*Safe Area Relative Margins가

기본적으로 체크되어있다. Safe Area를 고려하겠다!! 라는 속성인데 체크를 해제하게되면

Safe Area를 무시하는 값으로 Margin이 지정된다.

<img width="263" alt="스크린샷 2021-02-19 오후 6 44 09" src="https://user-images.githubusercontent.com/70311145/108487329-7c637400-72e2-11eb-9192-5006924a8f29.png">

ios11부터 바뀐 또 하나의 변경사항은 LayoutMargins 속성대신

Directional Margins 속성을 사용한다. 이 속성은 언어의 방향을 고려하기 위해

Left, Right 대신에 Leading, Trailing을 사용한다.

속성 또한 UIEdgeInsets이 아닌 [NSDirectionalEdgeInsets](https://developer.apple.com/documentation/uikit/nsdirectionaledgeinsets)이다.

Layout Margins에서 Language Directional을 선택하게 되면

Leading과 Trailing으로 변경되고 값은 그대로 남아있다.

<img width="260" alt="스크린샷 2021-02-19 오후 9 14 59" src="https://user-images.githubusercontent.com/70311145/108503336-8a6fbf80-72f7-11eb-94ad-5137e09644d7.png">

Directional은 ios11 버전 이상부터 사용가능하기에 그 이하 버전으로 앱을 배포할 때에는

호환성 문제에 대해 주의해야한다.

ios11 버전에서는 Directional Layout Margins를 사용하고,

이전 버전에서는 Layout Margins을 사용하게 하는 것이 중요하다.

Fixed와 Language Directional중 하나만 선택가능하기에 코드를 통해 처리해야한다.

```swift
if #available(ios 11.0, *) {
  view.directionalLayoutMargins = NSDirectionalEdgeInsets(top:leading:bottom:trailing:)
} else {
  view.layoutMargins = UIEdgeInsets(top:left:bottom:right:)
}
```

---

Margin을 기준으로 배치하는 것과 Bound를 기준으로 배치하는 것은 큰 차이를 가지고 있다.

Margin은 safe area 또는 super view의 영향을 받을 수 있다.

제약을 추가할 수 있는 핀 버튼을 클릭하면 Constrain to margins를 체크할수 있는 부분이 있다.

체크를 하게되면 뷰의 margin이 safe area를 고려하여 설정이 되고,

체크를 해제하고 제약을 주게되면 margin을 무시하고 Bound를 기준으로 배치된다.

Bound를 기준으로 배치할 때에는 네비게이션 바 또는 탭바같은 시스템 뷰와 겹칠 수 있다.

<img width="267" alt="스크린샷 2021-02-19 오후 9 44 29" src="https://user-images.githubusercontent.com/70311145/108506153-b55c1280-72fb-11eb-8d24-41d712d693bd.png">

또한 위에서 보았던 루트 뷰의 사이즈 인스펙터에서 Directional Layout Margins를 선택 후

값을 변경해도 Bound를 기준으로 배치된 뷰는 영향을 받지 않는다.

### VC에서 Margins를 변경할 때 주의할 점

![스크린샷 2021-02-19 오후 10 13 36](https://user-images.githubusercontent.com/70311145/108508823-bd1db600-72ff-11eb-8039-b7c1c8d8136d.png)

오렌지뷰는 루트뷰를 기준으로 top,leading,bottom,trailing은 모두 0으로 설정되어있고,

루트뷰의 Layout Margins를 모두 5로 설정했다.

<img width="267" alt="스크린샷 2021-02-19 오후 10 14 51" src="https://user-images.githubusercontent.com/70311145/108508931-e8080a00-72ff-11eb-80e2-ebcc7f929898.png">

하지만 오렌지뷰의 제약을 다시 보면 Top과 Bottom은 5로 되었지만

Leading과 Trailing은 5보다 큰 20으로 되어있는 것을 볼 수 있다.

이 값은 루트뷰의 minimum margins이다. Minimum margins보다 작은 값을 설정하면

설정된 margins 대신 minimum margins이 설정된다.

그 이유는 루트뷰의 내용이 적절히 표시되도록 보장하기 위해서이다.

minimum margins 대신 직접 입력한 margins를 사용하려면

VC가 minimum margins을 사용하지 않도록 설정해야 한다.

<img width="446" alt="스크린샷 2021-02-19 오후 10 21 23" src="https://user-images.githubusercontent.com/70311145/108509634-d115e780-7300-11eb-81ff-a0d85e53e2b6.png">

ios11부터 지원하기 때문에 배포상태에 따라 분기를 해주어야 한다.

---

## Layout Guides

ios11 이후 VC는 풀 스크린 방식을 사용한다. 시스템 뷰가 VC위에 표시되면서

뷰와 시스템 뷰가 겹치지 않게 하는 것이 중요해졌다.

레이아웃 가이드는 이러한 문제를 해결하기 위해 도입되었다.

Safe Layout Guides를 현재는 사용중이다.

파일 인스펙터를 보면 기본으로 Use Safe Area Layout Guides가 체크되어있다.

<img width="257" alt="스크린샷 2021-02-20 오전 1 19 09" src="https://user-images.githubusercontent.com/70311145/108531099-aab07600-7319-11eb-96e0-88bd5e882ab5.png">

Safe Layout Guides와 이 전 Layout Guides는 두가지 차이점이 있다.

첫번째 차이점은 Layout Guides는 VC의 속성이었지만 Safe Layout Guides는 View의 속성이다.

도큐먼트 아웃라인을 보면 Safe Area가 자동으로 추가되어 있다!

<img width="263" alt="스크린샷 2021-02-20 오전 1 22 10" src="https://user-images.githubusercontent.com/70311145/108531482-1266c100-731a-11eb-968a-95574c91339c.png">

Use Safe Area Layout Guides의 체크에 따라 달라지는 것을 볼 수 있다.

<img width="330" alt="스크린샷 2021-02-20 오전 1 24 37" src="https://user-images.githubusercontent.com/70311145/108531790-712c3a80-731a-11eb-8f45-065d16e1bade.png">

<img width="342" alt="스크린샷 2021-02-20 오전 1 24 43" src="https://user-images.githubusercontent.com/70311145/108531800-738e9480-731a-11eb-976e-0f6609e4f234.png">

두번째 차이점은 가이드의 영역이다. Safe Area는 Top과 Bottom으로 구분되지않은 하나의 영역이다.

Safe Area를 사용하는 경우에는 이전 버전과의 호완성을 유지한다.

ios11을 기준으로 이전 버전에는 Layout Guides로 자동으로 변환된다.

인터페이스 빌더에서는 오류없이 실행이 되지만 코드로 제약을 추가할 때에는 버전에 적합한 가이드를 사용해야 한다.

<img width="958" alt="스크린샷 2021-02-20 오전 1 36 33" src="https://user-images.githubusercontent.com/70311145/108533218-14318400-731c-11eb-90f5-73ef8787a75a.png">

**Layout Margins과 Safe Area 변경 될 때 활용할 수 있는 메서드**

```swift
layoutMarginsDidChange() // 뷰에 레이아웃 margins이 변경 될 때마다 호출

safeAreaInsetsDidChange() // SafeArea의 크기가 변경 될 때마다 호출

class EventsViewController: UIViewController {
  // 루트 뷰의 margins이 변경 될 때마다 호출
  override func viewLayoutMarginsDidChange(){
    super.viewLayoutMarginsDidChange()
  }
  // 루트 뷰의 Safe Area Inset이 변경 될 때마다 호출
  override func viewSafeAreaInsetsDidChange() {
    super.viewSafeAreaInsetsDidChange
  }

}
```

---

## [Adaptive Layout](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/adaptivity-and-layout/)

실행환경에 따라사 가장 적합한 방식으로 동작하는 앱의 기술을 구현학고,

모든 디바이스와 실행 환경에서 동작할 수 있는 하나의 UI를 개발하는 방법이

Adaptive Layout이다.

ios8 버전 이전에는 스토리보드에서 아이폰과 아이패드의 개발이 따로 분리되어있었지만

Adaptive Layout에서는 디바이스의 독립적인 Universal Storyboard를 사용한다.

Universal Storyboard는 다음의 중요한 세가지와 결합해서 모든 디바이스와

실행환경에 적용이 가능한 단일 Layout을 구현한다.

- Saze Class - 뷰를 배치할 수 있는 공간의 크기를 구분
- Trait Collection - 세부적인 실행환경을 구분
- Auto Layout

Adaptive Layout은 뷰의 계층과 화면의 전환에도 영향을 준다.

예를들어 아이폰 같은 작은 사이즈에서는 Push & Pop으로 화면 전환을 구현하고,

화면이 큰 아이패드의 경우 목록과 내용이 함께 표시된다.

### Size Class

Size Class는 인터페이스의 크기를 두개로 표현한다.

Class는 계층이나 종류를 의미하고(swift 문법의 class X)한다.

- **Regular** class - 너비나 높이가 비교적 크다는 것을 의미
- **Compact** class - 너비나 높이가 비교적 작다는 것을 의미
- **Any** class - 어느 한 방향의 클래스를 지정하지 않는다는 의미

Horizontal 또는 Vertical 사이즈 클래스를 통해서 너비와 높이에 해당하는 클래스를 개별적으로 지정한다.

더 상세한 디바이스의 Size Class는 H.I.G에서 확인할 수 있다.

<img width="698" alt="스크린샷 2021-02-20 오후 4 34 03" src="https://user-images.githubusercontent.com/70311145/108587865-80060200-7399-11eb-9422-3c341dd8b9ce.png">

### [Trait Collection](https://developer.apple.com/documentation/uikit/uitraitcollection)

Size Class 보다 더 상세학게 실행환경을 구분할 때 사용하며

ios 앱이 실행하는 환경에 대한 다양한 정보를 담고있다.

```swift
UITraitCollection
UITraitEnvironment
```

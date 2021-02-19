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

---
title: "ios) Layout - Margins & Guides"

categories:
  - AutoLayout

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-14

last_modified_at: 2021-02-14
---

# [Layout Margin](https://developer.apple.com/documentation/uikit/uiview/1622566-layoutmargins)

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

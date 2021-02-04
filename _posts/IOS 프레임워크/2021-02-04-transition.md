---
title: "UIKit) Transition"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-03

last_modified_at: 2021-02-03
---

Transition 알아보기

이 글의 전반적인 내용은 [KXCoding](https://kxcoding.com/)을 참고하였습니다.

---

## View Transition

### [Transition](https://developer.apple.com/documentation/uikit/uiview/1622574-transition)

view transition은 보통 동일한 컨테이너뷰에 속한 서브뷰 사이에 실행된다.

파라미터는 animate와 비슷한 형식으로 구현되어있다.

transition은 두가지 메서드 형식으로 되어있다.

---

with view를 통해 transition할 containerView을 전달한다.

<img width="510" alt="스크린샷 2021-02-04 오후 6 36 46" src="https://user-images.githubusercontent.com/70311145/106873770-24404580-6718-11eb-8157-5b5c25b160e6.png">

### [AnimationOptions](https://developer.apple.com/documentation/uikit/uiview/animationoptions)

transition 접두어를 가진 다양한 transition 타입이 선언되어있다.

애니메이션 블록 구현패턴은 크게 두가지가 있다.

**첫번째 패턴**으로는 사라지는 뷰를 뷰 계층에서 제거하고 새롭게 표시되는 뷰 계층에 추가한다.

뷰 계층에 추가된 뷰가 약한참조 (weak)로 연결되어 있고, 다른 소유자가 없다면

메모리에서 즉시 제거된다. (다시 연결하려면 아웃렛 연결시 강한참조로 연결)

**두번째 패턴**으로는 isHidden으로 토글한다.

뷰 계층에 영향을 주지않고 transition을 구현할 수 있다는 장점이 있다.

```swift
animations: {
    self.firstView.isHidden = !self.isHidden
    self.secondView.isHidden = !self.isHidden
}
```

---

from view, to view를 통해 전달하고

fromView에는 뷰 계층에서 제거할 뷰가 전달한다.

이 메서드는 animation 파라미터를 제공하지 않는다.

toView에서는 뷰 계층에 새롭게 추가할 뷰를 전달한다.

전달할 두개의 뷰는 반드시 동일한 뷰 계층에 포함되어 있어야한다.

<img width="505" alt="스크린샷 2021-02-04 오후 6 37 05" src="https://user-images.githubusercontent.com/70311145/106873776-260a0900-6718-11eb-899f-16140d5c2aad.png">

from에서 to로 뷰가 전달될 때에 fromView는 뷰 계층에서 제거된 후에 더이상 소유자가 없기 때문에

메모리에서 바로 제거된다. 그러므로 completion을 통해 반대로 뷰를 전달할 때에 이미 from에 있었던

뷰가 제거되었기에 오류가 발생한다. 이럴 때는 뷰를 강한참조로 연결해야 한다.

options에서 showHideTransitionViews를 추가하면 메서드가 뷰 계층을 조작하지 않고,

isHidden 속성을 토글한다. 이 옵션을 사용하게 되면 transition이 실행되는 동안에

뷰가 뷰 계층에서 제거되거나 추가되지 않기때문에 뷰가 약한참조로 연결되어도 문제가 없다.

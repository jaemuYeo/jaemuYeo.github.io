---
title: "UIKit) Animation"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-03

last_modified_at: 2021-02-03
---

Animation 알아보기

이 글의 전반적인 내용은 [KXCoding](https://kxcoding.com/)을 참고하였습니다.

# Animation

## [UIView Animation](https://developer.apple.com/documentation/uikit/uiview/1622515-animate)

UIView 클래스는 애니메이션에 사용되는 API를 타입메서드로 제공한다.

```swift
UIView.animate()
```

이 메서드를 활용하여 비교적 단순한 코드로 고품질의 애니메이션을 구현할 수 있다.

> 화면에 나열된 속성들이 애니메이션을 지원하는 속성.

<img width="640" alt="스크린샷 2021-02-02 오후 8 03 54" src="https://user-images.githubusercontent.com/70311145/106591829-15c82180-6592-11eb-8429-6f2e31226908.png">

<img width="750" alt="스크린샷 2021-02-04 오후 2 29 19" src="https://user-images.githubusercontent.com/70311145/106849122-7e7bdf00-66f5-11eb-872b-81550ad83ecd.png">

- duration - 애니메이션의 총 길이 (초), 지속시간

- animations - 뷰에 커밋 할 변경 사항이 포함 된 block object. null이 아니여야함.

- completion - 애니메이션 시퀀스가 ​​끝날 때 실행할 block object. 종료 후

애니메이션의 시작과 종료 함수

```swift
func startAnimating()
func stopAnimating()
```

### 간단한 애니메이션 실습해보기

<img width="607" alt="스크린샷 2021-02-04 오후 2 55 27" src="https://user-images.githubusercontent.com/70311145/106851163-17f8c000-66f9-11eb-8246-beb9c8873f38.png">

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/106851272-437baa80-66f9-11eb-82a2-43e0f30f9743.gif)

처음 시작을 하면 viewDidLoad에서 reset함수가 호출되고

가로 50 세로 50의 orangeView가 위치해있다.

animate 함수로 연결된 버튼을 클릭하면 orangeView가 루트뷰의 센터로 이동하면서

가로 100 세로 100으로 변경되면서 이동하게된다.

duration은 3초이고 animations에서는 alpha와 backgroundColor이 바뀌는 설정을 하였다.

마지막으로 completion을 통해 애니메이션 종료 후 다시 duration을 통해 3초동안 reset되었다.

**이 외 메서드**

스프링처럼 튕기는 애니메이션 구현

<img width="576" alt="스크린샷 2021-02-04 오후 4 35 13" src="https://user-images.githubusercontent.com/70311145/106859859-fb638480-6706-11eb-8d32-4a77305fd632.png">

현재 뷰에 대한 키 프레임 기반 애니메이션을 설정하는 데 사용할 수있는 애니메이션 구현

animate()를 통해 애니메이션 수가 늘어날수록 코드가 중첩이 되어 효율 적이지 않을 때 사용한다.

<img width="647" alt="스크린샷 2021-02-04 오후 5 30 47" src="https://user-images.githubusercontent.com/70311145/106865597-c0fde580-670e-11eb-9935-55abe4f13661.png">

[Animation Options](https://developer.apple.com/documentation/uikit/uiview/animationoptions)

여러가지 옵션들을 otions파라미터에서 배열로 받아서 구현할 수 있다.

---

## [UIViewPropertyAnimation](https://developer.apple.com/documentation/uikit/uiviewpropertyanimator)

Property Animator는 ios 10+에서부터 새롭게 도입되었다.

위의 내용인 UIViewAnimation을 대체하는 새로운 API를 제공한다.

UIViewAnimation에 비해 다양한 장점을 가지고 있다.

- 애니메이션 상태 제어
- 애니메이션 일시중지 또는 완전히 중지하는 메서드를 제공
- UIViewAnimation에서 제공하는 Timing Curve 모두 지원
- Bezier Timing Curve를 통해 직접만들 수 있는 API를 함꼐 제공
- 이미 시작 된 애니메이션에 새로운 애니메이션을 동적으로 추가할 수 있음
- Interactive Animations 구현 가능

Property Animator의 세가지 상태

- Inactive상태에서 시작 또는 정지를 하면 Active상태로 전환

- Active상태에서 애니메이션이 정상적으로 종료되면 다시 Inactive 상태로 전환

- Active상태에서 애니메이션을 직접 중지하면 Stopped상태로 전환( 애니메이션이 완료되지 않은 상태)

- Stopped상태에서 애니메이션을 다시 시작하려면 메서드를 호출해서 수동으로 완료 -> Inactive상태

### UIViewAnimation과 UIPropertyAnimation 코드 비교해보기

```swift
// UIViewAnimation
UIView.animate(withDuration: 3, delay: 0, option: [], animations: {
    self.colorView.backgroundColor = UIColor.orange
})

// UIPropertyAnimation
UIViewPropertyAnimator.runningPropertyAnimator(withDuration: 3, delay: 0, option: [], animations: {
    self.colorView.backgroundColor = UIColor.orange
})
```

구현방법이 비슷한 면이 있지만 UIViewPropertyAnimator는 Property처럼 사용하능하다.

애니메이션을 선언하고 여러 메서드를 붙여주어 상태를 제어할 수 있다.

start, pause, stop, finish 등의 제어가 가능하다.

```swift
let animator = UIViewPropertyAnimator(duration: duration, curve: .linear) {
    self.colorView.backgroundColor = UIColor.orange
}

animator.startAnimation(afterDelay: 2.0)
```

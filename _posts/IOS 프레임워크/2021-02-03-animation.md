---
title: "UIKit) Animation & Transition"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-03

last_modified_at: 2021-02-03
---

Animation & Transition 배워보기

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

---

## [UIViewPropertyAnimation](https://developer.apple.com/documentation/uikit/uiviewpropertyanimator)

---

---

# Transition

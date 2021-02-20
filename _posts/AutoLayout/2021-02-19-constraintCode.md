---
title: "ios) 코드로 작성하는 Constraint"

categories:
  - AutoLayout

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-19

last_modified_at: 2021-02-19
---

# 코드로 제약 추가방법 알아보기

## [NSLayoutConstraint](https://developer.apple.com/documentation/uikit/nslayoutconstraint)

스토리보드를 통한 제약추가 보다 난이도가 있고, 많은 코드를 필요로 하지만

동적으로 업데이트 되는 제약을 자유롭게 구현할 수 있는 장점이 있다.

### 자주 사용되는 코드

<img width="1008" alt="스크린샷 2021-02-20 오후 11 20 15" src="https://user-images.githubusercontent.com/70311145/108598654-3554ac00-73d2-11eb-9451-43a7d1427699.png">

첫번째 타입 메서드는 Visual Language를 통해 제약을 추가할 때 사용한다.

여러 제약을 동시에 추가할 수 있다는 장점과 코드의 가독성이 높아지지만

문자열로 코드를 작성하기 때문에 오타가 날 가능성과 디버깅이 어렵다는 단점이 있다.

두번째 생성자는 제약을 생성할 때 사용하는 기본적인 생성자이다.

파라미터에는 제약공식에 필요로 하는 것을 모두 받고있다.

![스크린샷 2021-02-20 오후 11 25 26](https://user-images.githubusercontent.com/70311145/108598772-ed825480-73d2-11eb-9b49-919e657775b3.png)

isActive 속성은 제약의 활성화 상태를 나타낸다.

뷰의 여러 제약중에서 활성화 된 제약만이 프레임 계산에 사용된다.

Adaptive Layout을 통해 활성화 하는 방식을 주로 사용한다.

activate와 deactivate 타입 메서드는 여러 제약의 활성화 상태를 동시에 변경할 때 사용한다.

**[NSLayoutConstraint.Attribute](https://developer.apple.com/documentation/uikit/nslayoutconstraint/attribute)** 열거형은 제약을 추가할 때 사용하는 다양한 속성들이 포함되어있다.

코드를 통해 제약을 추가할 때에는 이 열거형에 있는 속성들을 명시적으로 작성해주어야한다.

**[NSLayoutRelation](https://developer.apple.com/documentation/uikit/nslayoutconstraint/relation)** 또한 열거형으로 되어있고 세가지 맴버가 선언되어 있다.

<img width="590" alt="스크린샷 2021-02-20 오후 11 34 44" src="https://user-images.githubusercontent.com/70311145/108599396-3981c900-73d4-11eb-9bc4-9868b51f496a.png">

인터페이스 빌더에서 우선순위를 지정할 때에는 1000에서 0사이의 정수 값으로 선언하지만

코드로 설정할 때에는 **UILayoutPriority** 구조체로 설정해야한다.

## [NSLayoutAnchor](https://developer.apple.com/documentation/uikit/nslayoutanchor)

ios9 이 후 제약을 더 쉽게 추가하는 NSLayoutAnchor이 도입되었다.

NSLayoutConstraint에 비해 훨씬 짧은 코드를 작성할 수 있고, 가독성이 높아진다.

또한 TypeCheking을 통해 잘못된 제약으로 인한 오류를 사전에 방지해 준다.

<img width="658" alt="스크린샷 2021-02-20 오후 11 47 34" src="https://user-images.githubusercontent.com/70311145/108599698-050f0c80-73d6-11eb-979c-b6545025f48b.png">

NSLayoutAnchor클래스를 포함해 위 세가지 클래스들도 중요한 부분을 차지한다.

수평, 수직 방향의 제약을 추가할 때 필요한 메스드들을 제공하고,

너비와 높이의 제약을 추가할 때 추가로 필요한 메서드들도 제공하고 있다.

## [Visual Format Language](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/VisualFormatLanguage.html)

마크다운 만큼 비교적 단순한 언어이므로 사이트를 참조.

---

## 정리

- NSLayoutConstraint는 모든 제약을 추가할 수 있지만 코드가 길어지는 단점이 있다.

  디버깅이 어렵다.

- Visual Format Language는 단순한 표현식으로 제약을 추가할수 있고,

  한번에 다수의 제약을 추가할 수 있다.

  디버깅이 어렵다.

- NSLayoutAnchor는 가독성이 높고, 적은량의 코드로 제약을 추가할 수 있는 장점이 있다.

  디버깅이 쉽다.

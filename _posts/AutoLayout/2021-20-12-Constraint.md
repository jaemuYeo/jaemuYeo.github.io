---
title: "ios) Constraint(제약)"

categories:
  - AutoLayout

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-12

last_modified_at: 2021-02-12
---

# [Constraint](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/AnatomyofaConstraint.html#//apple_ref/doc/uid/TP40010853-CH9-SW1)

제약은 오토 레이아웃에서 핵심적인 내용이다.

Constraint는 NSLayoutConstraint 클래스로 구현되어있다.

[NSLayoutConstraint](https://developer.apple.com/documentation/uikit/nslayoutconstraint)

```swift
class NSLayoutConstraint : NSObject
```

---

## Equation

뷰 계층 구조의 레이아웃은 일련의 선형 방정식으로 정의된다.

제약은 요소사이의 간격을 설정하고 레이아웃 시스템은 제약을 기반으로 최종 프레임을 계산하고 배치한다.

프레임 계산에는 아래와 같은 공식이 사용된다.

<img width="613" alt="스크린샷 2021-02-12 오후 5 56 15" src="https://user-images.githubusercontent.com/70311145/107747969-ad303000-6d5b-11eb-8f83-2876760d636d.png">

```
item.attribute1 = muliplier * item2.attribute2 + constant
item.attribute1 >= muliplier * item2.attribute2 + constant
item.attribute1 <= muliplier * item2.attribute2 + constant
```

Item1 - 방정식의 첫 번째 항목이다. 항목은 뷰 또는 레이아웃 가이드이어야 한다.

Attribute1 - item1에 제한 될 속성이다. (제약을 지정할 속성)

Relationship - 왼쪽과 오른쪽 사이의 관계

Multiplier - Attribute2의 값에 이 부동 소수점 수를 곱한다. 기본값은 1.0이다.

Item2 - 방정식의 두 번째 항목이다. 첫번째 Item과 달리 비워 둘 수 있다.

Attribute2 - 두 번째 항목에 제한 될 속성이다. Item2가 비어 있으면 값은 Not an Attribute이다.

Constant - 상수, 부동 소수점 오프셋

### 공식 알아보기

캔버스에 뷰를 올리고 Top은 100, Leading은 50으로 제약을 추가한다.

<img width="747" alt="스크린샷 2021-02-12 오후 6 45 52" src="https://user-images.githubusercontent.com/70311145/107752895-b375da80-6d62-11eb-8d0a-cdc1152b69df.png">

Document Outline을 보면 위에서 설정한 제약이 방정식으로 표현되어있다.

Multiplier는 기본 값인 1.0으로 지정되어 있어 생략된다.

<img width="329" alt="스크린샷 2021-02-12 오후 6 47 57" src="https://user-images.githubusercontent.com/70311145/107753010-d7d1b700-6d62-11eb-97f7-08a40a20457a.png">

경우에 따라서 레이아웃 가이드와 같은 기준점을 지정할 수 있고, 너비와 높이를 지정할 때에는

Item2를 지정하지 않기도 한다.

Attribute는 마진을 나타내는 속성이다. 보통은 두 뷰의 사이를 나타내는 속성으로

leading, top, trailing, bottom, left, right 속성이 있다.

---

## Leading, Top, Trailing, Bottom

<img width="267" alt="스크린샷 2021-02-12 오후 6 56 48" src="https://user-images.githubusercontent.com/70311145/107753906-161ba600-6d64-11eb-821c-c62f37f1088c.png">

입력 필드에는 기본적으로 가장 인접한 뷰와의 거리가 자동으로 입력되어 있고,

필요에 따라 원하는 값으로 지정할 수 있다.

<img width="341" alt="스크린샷 2021-02-12 오후 6 58 46" src="https://user-images.githubusercontent.com/70311145/107754096-59761480-6d64-11eb-8dcd-74aa0abc40ec.png">

입력 필드 옆에 화살표를 클릭하면 대상을 직접 지정할 수 있다.

특별한 이유가 없다면 Safe Area로 설정하는 것이 좋다.

아래 사진에스는 네 곳의 제약을 전부 16으로 지정해 주었다.

<img width="385" alt="스크린샷 2021-02-12 오후 7 01 28" src="https://user-images.githubusercontent.com/70311145/107754393-c25d8c80-6d64-11eb-8223-d93d88d1c471.png">

Document Outline에서 방금 추가한 제약을 확인해보면 뷰의 아래가아닌 루트 뷰의 아래 설정되어있다.

마진과 관련된 속성이나 두 뷰가 연관된 속성들은 가장 인접한 공통 뷰에 추가된다.

위에 추가한 제약은 루트뷰와 오렌지 뷰간의 제약이기 때문에 루트 뷰에 추가되었다.

방정식을 보는 방법에 익숙해지면 뷰에 추가되어있는 제약을 조금 더 빠르게 파악할 수 있다.

왼쪽에 표시된 제약의 아이콘을 보면 해당 제약에 연관된 아이콘으로 표시되어있다.

<img width="378" alt="스크린샷 2021-02-12 오후 7 03 18" src="https://user-images.githubusercontent.com/70311145/107754554-fb95fc80-6d64-11eb-8bdc-77aa16d6cf7c.png">

---

## Width, Height

너비와 높이의 제약을 추가할 때에는 하나의 뷰에 고정된 Constant 값으로 추가하거나

다른 뷰와의 관계나 비율을 추가할 수 있다.

Top과 Leading이 100으로 되어있고 너비와 높이가 각각 200인 ㄹ

<img width="609" alt="스크린샷 2021-02-12 오후 7 12 10" src="https://user-images.githubusercontent.com/70311145/107755505-3cdadc00-6d66-11eb-9844-b1b2f0904959.png">

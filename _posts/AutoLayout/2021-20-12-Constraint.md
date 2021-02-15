---
title: "ios) Constraint(제약)"

categories:
  - AutoLayout

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-13

last_modified_at: 2021-02-13
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

Item1 - 방정식의 첫 번째 항목이다. 항목은 뷰 또는 레이아웃 가이드이어야 한다.

Attribute1 - item1에 제한 될 속성이다. (제약을 지정할 속성)

Relationship - 왼쪽과 오른쪽 사이의 관계

Multiplier - Attribute2의 값에 이 부동 소수점 수를 곱한다. 기본값은 1.0이다.

Item2 - 방정식의 두 번째 항목이다. 첫번째 Item과 달리 비워 둘 수 있다.

Attribute2 - 두 번째 항목에 제한 될 속성이다. Item2가 비어 있으면 값은 Not an Attribute이다.

Constant - 상수, 부동 소수점 오프셋

---

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

Top과 Leading이 각각 100으로 되어있고, 너비와 높이가 각각 200인 Label이 있다.

<img width="609" alt="스크린샷 2021-02-12 오후 7 12 10" src="https://user-images.githubusercontent.com/70311145/107755505-3cdadc00-6d66-11eb-9844-b1b2f0904959.png">

빨간색 뷰를 클릭해서 제약 팝업을 보면 Top에 가장 인접한 Lable이 연결되어 있다.

때에 따라서 대상을 루트 뷰나 Safe Area로 변경할 수도 있다.

<img width="732" alt="스크린샷 2021-02-12 오후 7 17 40" src="https://user-images.githubusercontent.com/70311145/107756070-fe91ec80-6d66-11eb-9847-2400809602ed.png">

레드 뷰에서 Top과 Leading을 지정해주면 비쥬얼 인디케이터에서 빨간색으로 실선이 표시된다.

그 이유는 레드 뷰의 너비와 높이를 판단할 수 없기 때문이다.

<img width="364" alt="스크린샷 2021-02-12 오후 7 19 40" src="https://user-images.githubusercontent.com/70311145/107756233-46187880-6d67-11eb-85c7-d19ff7e3f285.png">

레드 뷰에 너비와 높이를 지정해주면 정상적으로 제약이 추가되고 오류가 발생하지 않는다.

Document Outline을 보면 뷰와 뷰끼리 연관되지 않은 height와 width 제약은 각각의 Label과 View의

아래쪽에 추가되고 두 뷰와의 관계를 나타내는 제약은 최상위 뷰의 아래에 추가된 것을 확인할 수 있다.

![스크린샷 2021-02-12 오후 7 25 54](https://user-images.githubusercontent.com/70311145/107756863-2766b180-6d68-11eb-8312-49061960e831.png)

---

## CenterX, CenterY

이번 제약은 가운데 정렬 제약이다. 수평과 수직방향으로 추가할 수 있고, 컨테이너를 기준으로

가운데 정렬하거나 두 개 이상의 뷰를 가운데 정렬 할 수 있다.

Align메뉴를 클릭하고 Horizontal과 Vertical을 체크해주면 루트 뷰를 기준으로 정렬을 해준다.

<img width="671" alt="스크린샷 2021-02-12 오후 7 31 07" src="https://user-images.githubusercontent.com/70311145/107757421-e02cf080-6d68-11eb-9b22-e90979ecd02c.png">

```
Tip. 너비와 높이의 제약을 주지 않았는데 오류가 발생하지 않는다??

Label과 같이 뷰의 내용을 통해 크기를 유추할 수 있는 경우에는
너비와 높이 제약을 생략할 수 있고 Intrinsic Content Size를 통해
뷰의 크기를 표현한다.
내용이 없는 일반적인 뷰는 너비와 높이를 항상 추가해주어야 오류가 발생하지 않는다.
```

이번에는 그린 뷰에 Top과 너비,높이 제약을 추가한다.

<img width="693" alt="스크린샷 2021-02-12 오후 7 37 36" src="https://user-images.githubusercontent.com/70311145/107758204-e7a0c980-6d69-11eb-8840-18914b524d90.png">

그리고 그린 뷰에서 Label로 컨트롤 드래그해서 Center Horizontally를 선택하면 두 뷰가 가운데 정렬된다.

<img width="417" alt="스크린샷 2021-02-12 오후 7 38 25" src="https://user-images.githubusercontent.com/70311145/107758202-e5d70600-6d69-11eb-81cd-c3e93402fbd5.png">

또 다른 방법으로는 정렬 할 두 뷰를 모두 선택하고 Align메뉴에서

Vertical Centers 또는 Horizontal Centerrs를 통해 정렬을 하는 방법도 있다.

<img width="652" alt="스크린샷 2021-02-12 오후 7 42 18" src="https://user-images.githubusercontent.com/70311145/107758584-70b80080-6d6a-11eb-8599-0c7de08b05e3.png">

Document Outline을 보면 width, height와 달리 centerX, centerY 제약은 항상 공통된

상위 뷰에 추가된다. 현재는 모두 루트 뷰 아래쪽에 추가되어있다.

<img width="371" alt="스크린샷 2021-02-12 오후 7 44 05" src="https://user-images.githubusercontent.com/70311145/107758747-ae1c8e00-6d6a-11eb-8d4a-dc9780f22b7c.png">

---

## AspectRatio (종횡비)

종횡비는 너비나 높이를 기준으로 나머지 부분이 계산되는 제약이기에 반드시 width, height 제약을 추가해야한다.

가운데 정렬을 해주고 Aspect Ratio항목을 선택한다.

<img width="302" alt="스크린샷 2021-02-12 오후 7 50 26" src="https://user-images.githubusercontent.com/70311145/107759454-af01ef80-6d6b-11eb-904c-e145da49215c.png">
<img width="265" alt="스크린샷 2021-02-12 오후 7 50 36" src="https://user-images.githubusercontent.com/70311145/107759458-b0cbb300-6d6b-11eb-9d9c-3e5125eac60b.png">

비쥬얼 인디케이터를 보면 너비와 높이 제약이 추가된 것 처럼 보이지만 Aspect Ratio제약이다.

종횡비를 계산할 수 있는 기준이 없기때문에 현재는 제약 오류가 발생한다.

<img width="298" alt="스크린샷 2021-02-12 오후 7 51 08" src="https://user-images.githubusercontent.com/70311145/107759463-b1fce000-6d6b-11eb-9aca-0b7abf938706.png">

뷰에 너비 제약을 추가하게 되면 모든 제약 오류가 사라지고,

뷰의 높이는 뷰의 width 제약과 Aspect Ratio제약을 기준으로 계산된다.

이와 같이 Aspect Ratio를 추가할 때는 너비 또는 높이의 기준을 통해 계산한다는 것을 알고있어야 한다.

<img width="294" alt="스크린샷 2021-02-12 오후 8 53 58" src="https://user-images.githubusercontent.com/70311145/107765012-71ee2b00-6d74-11eb-96bf-fb1a9f97b54e.png">

---

## Baseline

완쪽의 Label에 Top과 Bottom 제약을 추가하고 오른쪽 Label에서 컨트롤 드래그를 통해

왼쪽과 Horizontal Spacing, First Baseline 제약을 추가하면 정상적으로 제약이 추가된다.

<img width="340" alt="스크린샷 2021-02-12 오후 9 04 07" src="https://user-images.githubusercontent.com/70311145/107765873-efff0180-6d75-11eb-8f69-28118cd245d3.png">

결과를 보면 프레임이 아닌 Label이 출력하고 있는 텍스트를 기준으로 정렬된다.

즉, 프레임이 아니라 뷰의 내용으로 정렬 된다.

<img width="302" alt="스크린샷 2021-02-12 오후 9 04 39" src="https://user-images.githubusercontent.com/70311145/107765883-f2615b80-6d75-11eb-8a2a-15300e0603da.png">

---

## 공식 알아보기

위에서 잠깐 지나갔던 내용중에는 다음과 같은 세개의 공식이 있다.

### Relation

<img width="387" alt="스크린샷 2021-02-12 오후 9 34 24" src="https://user-images.githubusercontent.com/70311145/107768714-3c4c4080-6d7a-11eb-9019-7af67decf084.png">

- Equal(=)

- Less Than or Equal (>=)

- Greater Than or Equal (<=)

아래의 Label은 Top, Leading, Bottom이 각각 설정 되어있고, height가 36으로 설정되어있다.

![스크린샷 2021-02-12 오후 9 17 42](https://user-images.githubusercontent.com/70311145/107767093-cf37ab80-6d77-11eb-8504-a9826653e073.png)

Relation Equal 텍스트에서 height 제약을 선택하고 인스펙터에서 Relation을

Less Than or Equal로 바꿔주면 Label의 높이가 텍스트를 표시하는데 필요한 Intrinsic Size로 표시된다.

<img width="415" alt="스크린샷 2021-02-12 오후 9 20 25" src="https://user-images.githubusercontent.com/70311145/107767321-26d61700-6d78-11eb-9027-93c794952843.png">

이번에는 Relation에서 Greater Than or Equal로 설정해주고

제일 아래에 있는 Label의 Bottom을 0으로 설정해주면 아래와 같이 나타난다.

밑에 두 Label의 Relation은 Equal이기 때문에 항상 설정된 Constant로 표시되지만

첫번째 Label은 Greater Than or Equal로 설정되어 있기 때문에

height인 36포인트보다 큰 값을 표시한다.

<img width="628" alt="스크린샷 2021-02-12 오후 9 24 56" src="https://user-images.githubusercontent.com/70311145/107767909-06f32300-6d79-11eb-8277-cc90d5bc9725.png">

<img width="343" alt="스크린샷 2021-02-12 오후 9 26 02" src="https://user-images.githubusercontent.com/70311145/107767899-05295f80-6d79-11eb-876b-6c124ede76e6.png">

---

### Multiplier

<img width="372" alt="스크린샷 2021-02-12 오후 9 34 42" src="https://user-images.githubusercontent.com/70311145/107768719-3d7d6d80-6d7a-11eb-8ef9-82f2caf01fce.png">

Multiplier는 제약 공식에서 두번째 항목에 적용할 승수를 나타내고 기본값은 1이다.

제약을 추가할 때 비율을 지정할 수 있다고 생각하면 이해하기 쉽다.

그린 뷰에는 너비와 높이가 지정되어 있고, x,y축의 가운데 정렬이 되어있다.

오렌지 뷰에는 그린뷰와의 간격곽 Equal width, Equal height가 설정되어있다.

<img width="306" alt="스크린샷 2021-02-12 오후 9 42 29" src="https://user-images.githubusercontent.com/70311145/107769371-3acf4800-6d7b-11eb-8ce7-7ed16e2087d6.png">

오렌지 뷰를 선택 후 사이즈 인스펙터에서 Equal height의 Edit항목을 선택하면

Multiplier의 값이 기본 값인 1로 설정되어 있는데 아래와 같이 2로 바꿔주면

그린 뷰의 height의 두배 값으로 늘어난 것을 볼 수 있다.

그리고 제약의 이름이 Proportional Height to: 로 변경되었다.

<img width="776" alt="스크린샷 2021-02-12 오후 9 44 34" src="https://user-images.githubusercontent.com/70311145/107769551-82ee6a80-6d7b-11eb-913a-28d6fdeb0d19.png">

이번에는 오렌지 뷰의 Equal width 값을 0.5로 주면 그린 뷰 너비의 절반으로 표시되고

제약의 이름이 Proportional Width to: 로 변경되었다.

<img width="823" alt="스크린샷 2021-02-12 오후 9 47 28" src="https://user-images.githubusercontent.com/70311145/107769852-eaa4b580-6d7b-11eb-8070-04bb56e8f3e7.png">

Multiplier의 값을 0.5와 같이 실수로 지정할 수도 있지만 가능하다면 정수로 지정하는 것이 좋다.

계산과정에서 발생할 수 있는 오차를 줄일 수 있기 때문이다.

위의 방식에서는 공식에 있는 Item2에 그린 뷰를 넣고 Item1에 오렌지 뷰를 너비를 계산했다.

Item1과 Item2를 바꾸고 Multiplier를 2로 바꾸면 실수로 지정했던 방법과 동일한 방법으로 구현할 수 있다.

오렌지 뷰의 사이즈 인스펙터에서 Proportional Width to 항목을 더블클릭하면

제약의 속성을 변경할 수 있는 화면으로 전환된다.

First Item은 공식에서의 Item1을 의미하고, Second Item은 공식에서의 Item2를 의미한다.

<img width="130" alt="스크린샷 2021-02-12 오후 10 07 18" src="https://user-images.githubusercontent.com/70311145/107771819-b1217980-6d7e-11eb-9b58-11e39699e5d8.png">

First Item에서 Recerse First And Second Item을 클릭하면

Multiplier의 값이 2로 변경된다. 오토레이아웃 입장에서 보면 오렌지 뷰의 너비를 설정할 때

'오렌지 뷰의 너비는 그린 뷰의 절반이다'라고 설정하는 것과

그린 뷰는 오렌지 뷰 너비의 두배이다'라고 설정하는 것이 동일하다.

마찬가지로 그린 뷰와 오렌지 뷰의 수직 여백을 추가할 때 그린 뷰의 Bottom 제약을 추가하는 것과

오렌지 뷰의 Top 제약을 추가하는 것 또한 동일하다.

<img width="253" alt="스크린샷 2021-02-12 오후 10 08 52" src="https://user-images.githubusercontent.com/70311145/107772000-f645ab80-6d7e-11eb-8937-615baa63b4ac.png">

---

### Constant

Constant를 번역하면 상수이지만 평소에 알고있던 상수는 값을 변경할 수 없다의 뜻을 가지지만

다른 속성들은 제약을 추가한 후에 변경할 수 없지만 Constant는 제약을 생성한 후에도 변경할 수 있다.

그래서 런타임에 제약을 업데이트하는 용도로 자주 활용된다.

<img width="375" alt="스크린샷 2021-02-12 오후 9 35 08" src="https://user-images.githubusercontent.com/70311145/107768722-3e160400-6d7a-11eb-8963-b79e9799d37a.png">

인터페이스에는 오렌지 뷰가 있고 수직, 수평 가운데 정렬과 너비와 높이가 설정되어있다.

<img width="237" alt="스크린샷 2021-02-12 오후 11 46 38" src="https://user-images.githubusercontent.com/70311145/107782567-91914d80-6d8c-11eb-83f1-7f86f32a336d.png">

Width Equals의 Edit를 보면 Constant에 240의 값이 입력되어있다.

Width나 Height의 경우 Constant 값 그 자체가 최종값이 된다.

<img width="246" alt="스크린샷 2021-02-12 오후 11 21 30" src="https://user-images.githubusercontent.com/70311145/107779678-0e222d00-6d89-11eb-99e4-4d8bf8b666fb.png">

그래서 Constant 값을 400으로 바꾸면 Width 제약이 400 포인트로 변경된다.

<img width="750" alt="스크린샷 2021-02-12 오후 11 23 33" src="https://user-images.githubusercontent.com/70311145/107779899-57727c80-6d89-11eb-82f6-9bb7f480c1f8.png">

이번에는 Align Center X의 Constant 값을 30으로 가운데 정렬 된 상태에서

30포인트만큼 오른쪽으로 이동한다. 이러한 경우에는 최종값이 아닌

정렬 후에 부가적으로 추가할 값이 된다.

![스크린샷 2021-02-12 오후 11 25 47](https://user-images.githubusercontent.com/70311145/107780156-aae4ca80-6d89-11eb-9aee-7c818838f2ac.png)

반대로 음수를 입력하면 가운데 정렬 된 상태에서 왼쪽으로 이동하게 된다.

하지만 Constant 값은 가능한 0이나 양수로 지정하는 것이 좋다.

그래서 옳바른 방법으로는 Multiplier에서 했던 것 처럼 First Item과 Second Item을 스위치하고,

Constant 값을 양수로 설정하는 것이 좋다.

코드를 통해 width제약과 height제약을 변경하는 것을 알아보자!

씬에 추가한 모든 것들은 아웃렛으로 연결할 수 있고, 제약 또한 마찬가지다.

추가된 제약에서 width와 height를 아웃렛으로 연결해주고 직접 접근해서 Constant 값을 변경하면 된다.

아래의 코드를 통해 changeFrame 버튼을 누르면 orangeView의 너비와 높이가 각각 100으로 변경된다.

<img width="528" alt="스크린샷 2021-02-12 오후 11 38 34" src="https://user-images.githubusercontent.com/70311145/107781636-7245f080-6d8b-11eb-8955-33c2fe9d4283.png">

---

### Priority (우선 순위)

Priority 속성은 1000 ~ 1 사이의 값으로 제약의 우선순위를 지정한다.

1000은 필수 제약을 의미하고 이보다 작은 값은 모두 옵션 제약이 된다.

오렌지 뷰가 있고 수직, 수평 가운데 정렬과 너비와 높이가 설정되어있다.

<img width="237" alt="스크린샷 2021-02-12 오후 11 46 38" src="https://user-images.githubusercontent.com/70311145/107782567-91914d80-6d8c-11eb-83f1-7f86f32a336d.png">

제약을 추가할 때는 일반적으로 제약의 종류별로 하나씩 추가한다.

하지만 경우에 따라 같은 종류의 제약을 두개이상 추가할 수 있다.

기존에 너비 제약이 추가되어있는 상태에서 또 하나의 100의 값인 너비 제약을 추가하면

Equal 뱃지를 보면 Relation이 Greater Than or Equal로 설정되어있다.

보통 제약을 추가하면 Relation이 Equal로 추가되는데 같은 제약을 서로다른 Constant 값으로

추가하면 제약이 충돌하므로 Xcode에서는 제약 충돌을 방지하기 위해 Greater Than or Equal지정한 것이다.

<img width="629" alt="스크린샷 2021-02-12 오후 11 49 40" src="https://user-images.githubusercontent.com/70311145/107782938-03699700-6d8d-11eb-8e43-7fc47797000d.png">

두번째로 추가헀던 너비의 제약을 선택후 Relation을 Equal로 설정하고

Priority 값을 999로 설정하게되면 우선순위로 설정된 첫번째 너비의 제약 값으로 남아있다.

프레임을 계산할 때 제약의 우선순위를 통해서 어떤 제약을 선택해야 하는지 확실하게 판단할 수 있기 때문이다.

Constant가 100인 제약은 여전히 뷰에 추가되어 있지만 우선순위가 더 높은 제약이 있고

다른 제약에 영향을 주지 않으므로 프레임 계산에서 무시된다.

<img width="819" alt="스크린샷 2021-02-12 오후 11 55 24" src="https://user-images.githubusercontent.com/70311145/107783587-c9e55b80-6d8d-11eb-9594-8864bf1602a7.png">

Document Outline에서 제약의 이름을 보면 @999가 추가되어 있다.

제약이 옵션 제약인 경우에는 우선순위가 함께 표시된다.

<img width="249" alt="스크린샷 2021-02-12 오후 11 59 12" src="https://user-images.githubusercontent.com/70311145/107784033-51cb6580-6d8e-11eb-80a8-361c914fde62.png">

코드를 통해 Priority 속성을 버튼을 통해 토글하는 방법을알아보자!

우선 순위를 생성자로 전달해서 UILayoutPriority 인스턴스를 만들고, 이 인스턴스를 Priority 속성에 할당하면 된다.

우선 순위가 1000이었던 너비의 Prority를 800으로 설정해주고나서

<img width="260" alt="스크린샷 2021-02-13 오전 12 26 48" src="https://user-images.githubusercontent.com/70311145/107787240-2d718800-6d92-11eb-96ac-cdd2d8dd134a.png">

코드를 통해 우선순위를 동적으로 변경할 때에는 제약의 우선순위를 1000보다 작은 값으로

설정해두어야 오류가 나지 않는다.

<img width="1015" alt="스크린샷 2021-02-13 오전 12 23 16" src="https://user-images.githubusercontent.com/70311145/107786920-c9e75a80-6d91-11eb-9379-e828d4f0b4f8.png">

Toggle 버튼을 클릭하면 두 제약의 우선순위가 변경되면서 UI가 동적으로 업데이트 된다.

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/107787045-eedbcd80-6d91-11eb-9034-ac61d00310b2.gif)

Priority의 패턴을 잘 활용하면 조건에 따라서 동적으로 업데이트 되는 UI를 다양하게 구현할 수 있다.

---

## Intrinsic Content Size

오토레이아웃은 뷰의 크기를 계산할 때 먼저 width, height 제약을 확인한다.

두 제약이 존재하지 않는다면 다른 제약이 통해 크기를 계산할 수 있는지를 확인한다.

여전히 크기를 계산할 수 없다면 뷰가 출력하려는 내용을 통해 크기를 계산한다.

옳바른 크기를 얻었다면 그 크기로 뷰를 출력하고, 얻지 못했다면 제약 오류가 발생한다.

Intrinsic Content Size는 뷰의 내용을 출력하는데 필요한 크기이다.

Intrinsic Content Size로 뷰를 출력하는 경우에는 내부적으로

Content Size Layout Constraint 제약이 자동으로 추가된다.

예를들어 루트 뷰안에 오렌지뷰를 올리고 Leading, Top의 제약만 추가했을 때에는

너비와 높이의 값을 파악할 수 없기 때문에 제약 오류가 발생한다.

<img width="357" alt="스크린샷 2021-02-13 오후 6 23 10" src="https://user-images.githubusercontent.com/70311145/107846636-9acff800-6e28-11eb-9353-d24d30420a65.png">

너비와 높이의 제약을 주게되면 제약이 정상적으로 추가되는 것을 확인 할 수 있다.

<img width="683" alt="스크린샷 2021-02-13 오후 6 23 36" src="https://user-images.githubusercontent.com/70311145/107846639-9d325200-6e28-11eb-92b1-c854b2bb731f.png">

이번에는 버튼에 Leading, Top 제약만 주었더니 제약오류가 발생하지 않는다.

뷰와는 다르게 너비와 높이에 대한 값이 없지만 정상적으로 제약이 추가되는 것을 볼 수있다.

<img width="356" alt="스크린샷 2021-02-13 오후 6 24 33" src="https://user-images.githubusercontent.com/70311145/107846687-f0a4a000-6e28-11eb-8c87-468059d5301d.png">

버튼 안에 있는 타이틀을 지워도 너비와 높이가 각각 30인 만큼의 크기가 자동으로 지정된다.

이러한 이유는 버튼이라는 기능이 사용자에게 최소한의 터치를 제공해야하기 때문이다.

<img width="358" alt="스크린샷 2021-02-13 오후 6 24 47" src="https://user-images.githubusercontent.com/70311145/107846688-f1d5cd00-6e28-11eb-8d80-05b33af8b77b.png">

스위치도 버튼과 마찬가지로 Leading, Top의 제약만 주어도 제약오류는 발생하지 않는다.

스위치 오브젝트 같은 경우는 높이와 너비의 기본값이 지정되어있으므려 따로 제약을 추가하지 않아도 된다.

<img width="397" alt="스크린샷 2021-02-13 오후 6 29 22" src="https://user-images.githubusercontent.com/70311145/107846754-77f21380-6e29-11eb-9b94-4b64617f81f9.png">

너비와 높이를 100으로 지정해 주어도 제약은 바뀌지만 UI의 변화는 없는 것을 확인할 수있다.

<img width="664" alt="스크린샷 2021-02-13 오후 6 29 40" src="https://user-images.githubusercontent.com/70311145/107846756-79234080-6e29-11eb-9076-86bd0b85a6f4.png">

이 외에도 다양한 오브젝트들의 제약을 추가해보고 Intrinsic Size에 어떤 영향을 주는지 알아보는 것이 좋다.

---

## Content Hugging (CH) & Compression Resistance (CR)

<img width="466" alt="스크린샷 2021-02-13 오후 9 56 22" src="https://user-images.githubusercontent.com/70311145/107850515-56535500-6e46-11eb-89db-36a4c101e1d2.png">

두개의 속성을 보면 Priority가 붙어 있는데 위에서 보았던 제약의 우선순위처럼

1000에서 1사이의 값으로 지정할 수 있는 우선순위이다.

<img width="258" alt="스크린샷 2021-02-13 오후 9 12 02" src="https://user-images.githubusercontent.com/70311145/107849663-23a65e00-6e40-11eb-92ca-50147879c78c.png">

이 우선순위는 뷰를 배치할 수 있는 공간의 크기가 Intrinsic Size와 다를 때

너비와 높이 값이 커지거나 작아지는 우선순위를 지정한다.

CH와 CR 모두 수평과 수직 방향으로 하나씩 우선순위를 지정할 수 있고,

CH의 기본 값은 250 CR의 기본 값은 750이다.

Intrinsic Size를 가진 뷰가 동일 선상에 두개 이상 배치되어 있을 때 의미를 가지게 된다.

- Content Hugging - 프레임 확장에 대한 저항력

  늘어나지 않으려고 버티는 힘.

  CH의 우선 순위가 1000이라면 가장 높은 저항력을 가지는 것이고,

  어떠한 경우에도 너비나 높이가 Intrinsic Size를 초과하지 않는다.

  우선 순위가 낮아질수록 저항력도 낮아지고, Intrinsic Size를 초과할 가능성이 높아진다.

아래에는 Label과 TextField의 제약에 추가되어 배치되어있다.

현재 Intrinsic Size와 CH를 통해 계산된 너비를 가지고 있다.

현재 Label의 CH 값이 251, TextField의 CH 값이 250이로 설정되어 있어서

프레임 확장에 대한 저항력이 더 높은 Label이 Intrinsic Size로 표시되고,

상대적으로 낮은 TextField가 확장되어서 나머지 영역을 채우게 된다.

<img width="279" alt="스크린샷 2021-02-13 오후 9 24 07" src="https://user-images.githubusercontent.com/70311145/107849944-d4612d00-6e41-11eb-959d-d031746bb556.png">

TextField의 CH값을 260으로 바꾸게 되면 프레임 확장에 대한 저항력이 Label보다 높아지고

TextField는 Intrinsic Size로 표시되고, Label이 나머지 영역을 채운다.

<img width="276" alt="스크린샷 2021-02-13 오후 9 28 37" src="https://user-images.githubusercontent.com/70311145/107849999-7719ab80-6e42-11eb-8529-31438e454f11.png">

혹여나 두 우선순위의 값이 같으면 제약 오류가 발생하고, 이 오류를 해결하는 방법으로는

width을 추가하거나 Label과 TextField의 너비를 같게 만드는 Equal width 제약을 추가하는 것이다.

- Compression Resistance - 프레임 축소에 대한 저항력

  외부에서 압력을 줄 때 버티는 힘.

  우선 순위가 1000으로 지정되어 있다면 어떤 경우에도 클리핑 없이 표시되지만

  우선 순위가 낮아질 수록 프레임 축소에 대한 저항력이 낮아서

  클리핑이 발생할 수도 있고, 경우에 따라 제약 오류가 발생한다.

CR의 우선순위와 Width의 우선순위가 동일하다면 CR이 더 높은 우선순위를 가지게 된다.

코드를 통해 동적으로 변경하는 경우에는 우선순위 지정에 주의해야한다.

**UI를 설계할 때에는 되도록이면 CH, CR을 함께 고려해야하는 경우가 없도록해야한다.**

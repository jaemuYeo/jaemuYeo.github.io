---
title: "UIPickerView"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-08

last_modified_at: 2021-01-08

---

# PickerView

> 피커뷰는 슬롯머신 형태의 UI를 가지고있고, 휠을 돌려서 값을 선택한다.

cocoa tuch framework는 두가지의 슬롯머신을 제공한다.

1. Date Picker - 날짜나 시간 선택
2. Picker View - 범용적으로 사용 (다양한 데이터를 자유롭게 구현)

두 피커는 동일한 방식으로 동작하지만 구현에는 큰 차이가 있다.

데이터피커는 원하는 모드를 선택하기만 하면 UI와 데이터는 자동으로 구성된다.

피커에서 항목을 선택하면 **valueChanged** 이벤트가 전달되고

선택한 값을 가져올 때에는 Date값을 사용한다.

반면, 피커뷰는 표시할 값을 직접지정하며 경우에 따라 필요한 뷰를 직접 구성해야 한다.

---

선택이벤트는 델리게이트패턴으로 처리해야한다.

<img width="267" alt="스크린샷 2021-01-08 오전 7 11 03" src="https://user-images.githubusercontent.com/70311145/103950726-bdfbed80-5180-11eb-9293-9550611dbfe3.png">

라이브러리에서 인터페이스 빌더로 피커뷰를 끌어다 놓게되면

이렇게 기본 데이터가 표시되어 있는데 실제로 표시되는 데이터는 아니다.

<img width="257" alt="스크린샷 2021-01-08 오전 7 20 45" src="https://user-images.githubusercontent.com/70311145/103951471-141d6080-5182-11eb-8d5a-53907f11d1bf.png">

피커뷰의 속성을 보게되면 View 속성 이외에는 다른 특화된 속성이 없다.

피커뷰를 구현 할 때에는 모든 부분을 코드로 구현한다.

<img width="1022" alt="스크린샷 2021-01-08 오전 7 23 11" src="https://user-images.githubusercontent.com/70311145/103951628-665e8180-5182-11eb-93ed-78a75a7ae4fe.png">

피커뷰의 구현에 있어서 이 두가지가 핵심요소이다.

천천히 한번 알아보도록 하자.

<img width="351" alt="스크린샷 2021-01-08 오전 7 29 01" src="https://user-images.githubusercontent.com/70311145/103952300-86427500-5183-11eb-87b3-2d4586daa6ce.png">

라이브러리에서 뷰로 끌어다 놓은 피커뷰에 마우스 오른쪽 클릭을 하면 위와같은

커넥션패널이 뜨는데 dataSource와 delegate 두가지를 연결해준다.

동그라미 부분을 누르고

<img width="298" alt="스크린샷 2021-01-08 오전 7 33 21" src="https://user-images.githubusercontent.com/70311145/103952473-d3264b80-5183-11eb-8864-46a484c73234.png">

뷰의 윗부분에서 왼쪽의 아이콘으로 드래그해주면 된다.

스위프트파일의 해당 클래스 코드로 들어가서

<img width="819" alt="스크린샷 2021-01-08 오전 7 41 58" src="https://user-images.githubusercontent.com/70311145/103953191-03221e80-5185-11eb-922f-b542ed491d67.png">

extension을 통해 dateSource를 구현하고 필수매서드를 입력한다.

<img width="920" alt="스크린샷 2021-01-08 오전 7 46 38" src="https://user-images.githubusercontent.com/70311145/103953545-abd07e00-5185-11eb-9fdb-60b11ec2a945.png">

그리고 새로운 extension으로 Delegate를 구현한다.

<img width="354" alt="스크린샷 2021-01-08 오전 7 48 08" src="https://user-images.githubusercontent.com/70311145/103953656-dfaba380-5185-11eb-91f1-d5e7703b4f33.png">

짜잔!!!!!

간단한 메서드들을 구현하게 되면 해당 배열의 문자열이 피커뷰표시되고 휠로 선택할 수 있다.

회색으로 표시된 셀렉션 인디케이터는 선택된 항목을 강조한다.

인디케이터를 숨기는 방법은 제공하지 않으므로 위의 사진처럼 항상 표시되고 커스터마이징도 불가능하다.

이번에는 선택된 항목을 표시하는 메서드를 델리게이트를 통해 구현해 보자.

<img width="859" alt="스크린샷 2021-01-08 오전 7 55 56" src="https://user-images.githubusercontent.com/70311145/103954155-f69ec580-5186-11eb-856b-d74b1b4e2492.png">

델리게이트를 통해서 해당 배열을 확인하는 방법은 사용자가 항목을 직접 선택해야 메서드가 호출된다.

그래서 특정 시점에 선택되어있는 항목을 확인하는 것은 어렵다.

UIPickerView가 제공하는 메서드로 선택한 항목을 확인해보자.

<img width="466" alt="스크린샷 2021-01-08 오전 8 02 03" src="https://user-images.githubusercontent.com/70311145/103954552-d3284a80-5187-11eb-9153-0adc469f9785.png">

스토리보드에 버튼을 추가하고 피커와 버튼을 각각 아울렛, 액션으로 연결한 후 코드를 작성하였다.

선택한 항목이 없다면 "not found"를 출력하고, 항목이 있다면 그 항목을 콘솔에 출력하는 코드이다.

<img width="549" alt="스크린샷 2021-01-08 오전 8 05 28" src="https://user-images.githubusercontent.com/70311145/103954836-6497bc80-5188-11eb-8633-20f46c014d8b.png">

따란~~ Report버튼을 누르면 선택한 항목이 출력되는 것을 볼 수 있다.

보통 휠의 선택과 동시에 바로 사용해야한다면 위에서 했던 Delegate의 메서드 중

didSelectRow 메서드를 사용하고, 나머지 경우에는 뒤의 방식으로 구현한다.

---

이번에는 컴포넌트를 한개 더 추가하고 새로운 배열을 넣어보자.

<img width="546" alt="스크린샷 2021-01-08 오전 8 22 29" src="https://user-images.githubusercontent.com/70311145/103955909-b80b0a00-518a-11eb-8fe8-b5261d88db91.png">

해당 메서드의 리턴값을 2로 바꿔주고

<img width="810" alt="스크린샷 2021-01-08 오전 8 30 03" src="https://user-images.githubusercontent.com/70311145/103956378-c0177980-518b-11eb-8778-5f091475666a.png">

switch-case를 이용하여 해당 컴퍼넌트가 나타나도록 분기해야한다.

같은 배열을 다른 컴포넌트로 사용하는 경우에는 처음처럼 구현해도 되지만

다른 배열을 통해 다른 값을 보여주고 싶다면 이렇게 구현해야 한다.

다른 메서드들도 변경해주도록 한다.

<img width="924" alt="스크린샷 2021-01-08 오전 8 25 04" src="https://user-images.githubusercontent.com/70311145/103956458-e50bec80-518b-11eb-9545-291780d3fe06.png">

<img width="858" alt="스크린샷 2021-01-08 오전 8 31 56" src="https://user-images.githubusercontent.com/70311145/103956507-010f8e00-518c-11eb-81df-ff7013c6f23e.png">

<img width="549" alt="스크린샷 2021-01-08 오전 8 32 58" src="https://user-images.githubusercontent.com/70311145/103956566-27cdc480-518c-11eb-8ebe-3ab9a04d8ab0.png">

코드를 실행해 보면

<img width="548" alt="스크린샷 2021-01-08 오전 8 36 13" src="https://user-images.githubusercontent.com/70311145/103956794-9874e100-518c-11eb-9296-e47e9fb5593f.png">

두개의 컴포넌트가 생기고 각각 선택된 항목을 출력하는 것을 볼수있다!! 👏👏

---

### 참고 자료

- [UIPickerView](https://developer.apple.com/documentation/uikit/uipickerview)
- KXCoding 강의

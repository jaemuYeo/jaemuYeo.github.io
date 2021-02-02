---
title: "UIKit) TableView 알아보기 1"

excerpt: "tableview controller"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-19

last_modified_at: 2021-01-19
---

# [Table View](https://developer.apple.com/documentation/uikit/uitableview)

Table View는 세로방향으로 스크롤되는 목록을 구현할 때 사용한다.

Table View의 가장 기초가 되는 구현 순서.

1. Table View를 View에 배치 후 오토레이아웃 지정 (크기 설정)

2. 새로운 프로토타입 Cell을 추가하고 원하는 방식으로 구성

3. 프로토타입 Cell의 Identifier 이름을 지정

4. Table View의 DataSource를 지정 (Delegate)

5. 클래스를 익스텐션하고 UITableVIewDataSoruce 프로토콜을 선언 후 필수 메서드 구현

섹션과 셀로 구성되어있고 셀의 위치를 표현 할 때는 섹션 인덱스와 셀 인덱스를 모두 고려해야한다.

**IndexPath ( cell접근 방법 )**

- cell - Row Index ( indexPath.row )
- section - Section Index ( indexPath.section )

Table View는 [UITableViewDelegate](https://developer.apple.com/documentation/uikit/uitableviewdelegate) , [UITableViewDataSource](https://developer.apple.com/documentation/uikit/uitableviewdatasource) 를 통해 구현한다.

> 셀을 식별하기위해 문자열을 입력해야 한다. 이 식별자를 'Reuse Identifier'라고 부른다.

프로토콜을 채용하기 위해서는 클래스 밑에 **extension** 을 통해 구현하는 것이 좋다. (가독성)

```swift
extension tableViewController: UITableViewDataSource {

}

extension tableViewController: UITableViewDelegate {

}
```

---

## UITableViewDataSource 필수메서드

섹션에 표시할 셀 수를 리턴하는 메서드 (배열 또는 데이터의 인덱스 갯수)

<img width="750" alt="스크린샷 2021-01-19 오후 8 15 12" src="https://user-images.githubusercontent.com/70311145/105027484-2907c700-5a93-11eb-818e-4b0f7edfb1fa.png">

셀을 생성하고 셀에 표시할 데이터를 설정한 후 리턴하는 메서드

<img width="731" alt="스크린샷 2021-01-19 오후 8 18 45" src="https://user-images.githubusercontent.com/70311145/105027816-8f8ce500-5a93-11eb-87a9-fbef9313d049.png">

셀을 생성할 때는 테이블뷰에게 요청해야한다. 테이블뷰의 스크롤 성능을 높이기위해서

**재사용 메커니즘**을 사용한다.

테이블뷰는 재사용 큐를 관리하면서 셀 생성 요청이 있을 떄 마다 큐에 저장된 셀을 리턴한다.

요청 시점에 저장되어 있는 셀이 없으면 프로토타입 셀을 기반으로 새로운 셀을 생성한다.

> Tip. cellForRowAt 메서드는 최대한 가볍게 구현해야한다. (스크롤 성능때문에 비동기로 구현)

이 메서드는 지정된 재사용 식별자에 대해 재사용 가능한 테이블 뷰 셀 객체를 반환하고 테이블에 추가한다.

<img width="660" alt="스크린샷 2021-01-19 오후 8 23 06" src="https://user-images.githubusercontent.com/70311145/105028324-3bcecb80-5a94-11eb-8c0c-275874844f49.png">

indexPath를 통해 셀에 접근 할 수 있다. 셀에는 Label, Image 등이 있다.

---

## custom Accessory 스위치 구현

스토리보드에서 custom Accessory 설정이 불가능하기에 코드로 구현해야한다.

UITableViewCell을 상속하는 클래스를 만든 후 초기화 코드를 구현하는 방법을 사용해아한다.

테이블뷰와 셀을 루트뷰에 지정한 후에 UITableViewCell을 상속받는 클래스를 만들어준다.

<img width="717" alt="스크린샷 2021-01-20 오전 1 25 12" src="https://user-images.githubusercontent.com/70311145/105063422-10150b00-5abf-11eb-8391-743fd6945c1f.png">

awakeFromNib 메서드에 초기화 시키는 코드를 작성한다.

<img width="638" alt="스크린샷 2021-01-20 오전 1 24 51" src="https://user-images.githubusercontent.com/70311145/105063409-0db2b100-5abf-11eb-803d-377624b58bd6.png">

다시 돌아가 커스텀 할 셀 속성에서 Custom Class에 방금 초기화한 클래서를 지정해준다.

<img width="260" alt="스크린샷 2021-01-20 오전 1 25 32" src="https://user-images.githubusercontent.com/70311145/105063424-10ada180-5abf-11eb-8ba1-5c5c5f19905f.png">

셀의 Identifier를 지정해준 후 클래스에 UITableViewDataSource 프로토콜을 선언한다.

<img width="256" alt="스크린샷 2021-01-20 오전 1 28 37" src="https://user-images.githubusercontent.com/70311145/105063425-11463800-5abf-11eb-997c-6e25cabde0f8.png">

필수 매서드 구현 후 앱을 실행해주면 스위치 악세사리가 적용된것을 볼 수 있다.

Target - Action을 통한 액션구현도 가능하다.

<img width="849" alt="스크린샷 2021-01-20 오전 1 53 35" src="https://user-images.githubusercontent.com/70311145/105066676-60da3300-5ac2-11eb-8492-5505f8355b10.png">

<img width="568" alt="스크린샷 2021-01-20 오전 1 53 42" src="https://user-images.githubusercontent.com/70311145/105066687-63d52380-5ac2-11eb-9969-2cd8182c80c1.png">

---

## Custom Accessory View 구현해보기.

- Disclosure indicator - cell을 선택했을 때 push로 화면 전환될 때 사용.
- Detail Button - 상세정보를 모달 형태로 전달할 때 사용. (delegate를 통해 구현)
- Detail Disclosure - 위의 두 스타일을 모두 사용하는 것.
- Checkmark - 선택상태를 표시할 떄 사용.
- None - 기본 스타일

Custom Accessory View를 통해 이미지를 추가할 수 있다.

cellForRow(at:)메서드에서 구현하게 되면 오버헤드가 발생하므로

새로운 커스텀셀 클래스를 만들고 초기화 시점에 코드가 실행되도록 구현해야한다.

스토리보드에서 Table View와 Cell을 배치하고 각 cell의 identifier를

'cell' , 'cell2'로 지정한 후 새로운 viewController에 푸시와 모달 연결.

<img width="662" alt="스크린샷 2021-01-20 오후 8 16 49" src="https://user-images.githubusercontent.com/70311145/105167883-a51a1180-5b5c-11eb-8f02-00205d56f85f.png">

switch로 메서드의 indexPath.row에 접근하여

case 별로 텍스트와 악세사리 타입을 지정.

<img width="837" alt="스크린샷 2021-01-20 오후 8 17 14" src="https://user-images.githubusercontent.com/70311145/105167889-a6e3d500-5b5c-11eb-9f98-7a3b0a5d0d05.png">

UITableViewDelegate 프로토콜을 선언하고 Push와 Modal 실행 구현

<img width="815" alt="스크린샷 2021-01-20 오후 8 17 21" src="https://user-images.githubusercontent.com/70311145/105167894-a9462f00-5b5c-11eb-83a4-a6fd31e0f0c2.png">

Custom Accessory Image 구현 코드

<img width="620" alt="스크린샷 2021-01-20 오후 8 17 26" src="https://user-images.githubusercontent.com/70311145/105167897-a9dec580-5b5c-11eb-8711-8b958152d686.png">

## ![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/70311145/105167983-ce3aa200-5b5c-11eb-9cda-335407ee0a70.gif)

## Separator Inset. 개별 Cell 적용하기

<img width="844" alt="스크린샷 2021-01-20 오전 2 25 59" src="https://user-images.githubusercontent.com/70311145/105070641-f081e080-5ac6-11eb-9046-b47fd04b3984.png">

<img width="568" alt="스크린샷 2021-01-20 오전 2 26 04" src="https://user-images.githubusercontent.com/70311145/105070654-f4adfe00-5ac6-11eb-8cc4-73f43b3bfe0b.png">

재사용 메커니즘으로 인한 Inset이 다시 사용되는 것을 막기위해 초기화를 꼭 해줘야 한다.

tableView와 tableViewCell의 속성에서는 separator만 설정이 가능하다.

이미지나 높이를 직접 지정하고 싶다면 separator를 none으로 설정 후 커스텀 separator를 구현해야한다.

---

## Table View Cell

기능구현

1. 셀에 이미지 넣기
2. 셀을 클릭하면 푸시화면에 해당 셀 텍스트 넣기
3. 짝수 인덱스 셀에 Background Color 설정하기.
4. 델리게이트 구현하기.

<img width="793" alt="스크린샷 2021-01-20 오전 3 02 30" src="https://user-images.githubusercontent.com/70311145/105074666-047c1100-5acc-11eb-9272-85f2c448d28d.png">

<img width="616" alt="스크린샷 2021-01-20 오후 4 44 14" src="https://user-images.githubusercontent.com/70311145/105143172-d257c700-5b3e-11eb-9801-77b7967189b3.png">

.

<img width="428" alt="스크린샷 2021-01-20 오후 4 44 26" src="https://user-images.githubusercontent.com/70311145/105143175-d2f05d80-5b3e-11eb-9c0d-12d5886a3b35.png">

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/70311145/105075196-c8957b80-5acc-11eb-8170-e71c61bc50d6.gif)

### 사용한 메서드

지정된 셀의 인덱스 경로를 가져온다.

<img width="676" alt="스크린샷 2021-01-20 오후 4 32 57" src="https://user-images.githubusercontent.com/70311145/105143157-d1269a00-5b3e-11eb-82db-46a029e20fc6.png">

지정된 인덱스 경로에있는 테이블 셀을 반환

<img width="746" alt="스크린샷 2021-01-20 오후 4 24 40" src="https://user-images.githubusercontent.com/70311145/105143178-d388f400-5b3e-11eb-8043-c62cbafcc967.png">

tableView가 특정 행에 대한 셀을 그리려고한다는 것을 Delegate에게 알림

<img width="743" alt="스크린샷 2021-01-20 오후 4 38 41" src="https://user-images.githubusercontent.com/70311145/105143167-d257c700-5b3e-11eb-9329-8955132cd264.png">

Delegate에게 행이 선택되었음을 알림

<img width="625" alt="스크린샷 2021-01-20 오후 4 26 06" src="https://user-images.githubusercontent.com/70311145/105143180-d4218a80-5b3e-11eb-970c-e00bb2335b33.png">

셀을 선택한 상태에서 새로운화면으로 전환되기 직전에 호출

<img width="608" alt="스크린샷 2021-01-20 오후 4 30 01" src="https://user-images.githubusercontent.com/70311145/105143182-d4218a80-5b3e-11eb-892a-de3d3ad07fde.png">

---

## Self Sizing Cell

Self-Sizing Cell이란 Table View의 셀에 표시되는 내용이 보여지도록 자동으로 높이를 설정하는 것이다.

ios11버젼 이 후에는 sizing 속성의 automatic이 체크되어있고 기본 값 되어있으나,

이전 버젼의 SDK로 빌드할 때에나 평소에도 코드를 통해 두 속성의 값을 직접 설정할 수 있다.

지금보는 화면에서는 셀의 높이가 조절이 되지않아 텍스트가 잘려서 보인다.

이 경우에는 automatic의 문제가 아니라 Label의 라인 속성이 1로 되어있어서

0으로 바꿔주면 모든 텍스트가 보여지가 셀이 조절이 된다.

<img width="568" alt="스크린샷 2021-01-20 오후 8 59 33" src="https://user-images.githubusercontent.com/70311145/105172620-3ab89f80-5b63-11eb-9090-f81b22fae2ba.png">

Table View 속성이 기본으로 제공되는 셀의 속성일 때에는 Label의 속성만 고려하면 되지만

Custom Cell을 직접 구현할 때에는 높이의 제약을 지정해주는 것이 매우 중요하다.

Table View에 표시되는 내용의 높이를 예측 할 수 없다면 Self-Sizing Cell을 사용하지만

모든 셀의 높이가 동일하다면 높이를 직접 지정해주는 것이 좋은 선택이다.

<img width="1088" alt="스크린샷 2021-01-21 오전 12 28 07" src="https://user-images.githubusercontent.com/70311145/105197082-998c1200-5b7f-11eb-8f83-22dbfe5334e0.png">

UITableViewDelegate를 통해 개별적으로 셀에 접근해 높이를 지정가능하다.

위 코드는 0번째 인덱스에 접근해 높이를 100으로 제한하고 나머지는 자동으로 계산되게 하였다.

<img width="568" alt="스크린샷 2021-01-21 오전 12 28 16" src="https://user-images.githubusercontent.com/70311145/105197100-9d1f9900-5b7f-11eb-8edc-da7d1646cf0d.png">

코드 결과를 보면 첫번째 셀은 100으로 지정된 높이로 표시되고

그 밑에 셀은 자동으로 조절이 된 것을 확인할 수 있다.

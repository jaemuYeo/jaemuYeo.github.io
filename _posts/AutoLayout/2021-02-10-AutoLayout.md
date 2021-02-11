---
title: "ios) 오토레이아웃 1"

categories:
  - AutoLayout

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-10

last_modified_at: 2021-02-10
---

# [Auto Layout](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/index.html)

## Overview

오토 레이아웃은 해당 뷰에 적용된 제약 조건에 따라 뷰 계층 구조에있는 모든 뷰의 크기와 위치를 동적으로 계산한다.

지금까지 나온 모든 디바이스와 앞으로 나올 디바이스의 해상도와 스케일을 모두 암기할 필요는 없다.

오토레이아웃을 통해 제약을 추가하는 방법만 잘 알고있으면 모든 해상도에서 UI를 구현할 수 있다.

UI를 구성하는 방식에는 변화가 있다.

---

- **Frame-Based Layout**

  가장 먼저 사용된 방식이다.

  프레임의 상위 뷰에 좌표시스템에서 특정 뷰의 위치와 크기를 나타내는 용어이다.

  개발자가 프레임을 직접 제작하고 설정해야하는 방식이다.

  하나의 해상도만 존재하던 시절에는 문제가 없었지만 요즘같이 다양한 해상도가 나오면서

  프레임을 제작하는 과정이 복잡해졌다. 특히 상위 뷰의 크기변화에 따라 하위 뷰의 크기를 변경하는 작업이

  많이 어려워 졌다. 그래서 나온 방법이 Auto resizing mask이다.

  Auto resizing mask는 상위 뷰의 프레임이 변경될 때에 하위 뷰의 프레임이 변경되는

  규칙을 미리 지정된 여섯개의 비트마스크로 지정한다.

  Auto resizing mask을 통해서 프레임을 계산하는 부담은 줄었지만 모든 문제를 해결하지는 못했다.

- **Auto Layout**

  위 문제를 해결하기 위해 나온 방식이 오토 레이아웃이다.

  이 방식이 나오면서 Frame-Based Layout과 Auto resizing mask가 완전히 사라진 것은 아니다.

  오토 레이아웃에서 해결할 수 없는 약간의 문제를 위의 방식으로 해결할 수 있다.

  Auto resizing mask는 UI프로토타이핑에 활용되고 있다.

  오토 레이아웃은 UI를 구성하는 뷰의 크기나 위치를 다른 요소와의 관계를 나타내는 특별한 규칙을 통해

  자동으로 계산하고 배치하는 기술이다.

  Constraints(제약)는 오토 레이아웃에서 가장 중요한 개념이다.

  Constraints를 기반으로 최종 프레임에 뷰를 배치한다.

- **Adaptive Layout**

  IPhon 8이 나오던 2014년도에 UI구성 방식에 또 다른 방식이 등장한다.

  애플은 Adaptive Layout 통해 모든 디바이스의 해상도에 대응하는

  하나의 UI를 개발할 수 있도록 Size Class와 Trait Collection을 도입했다.

  이 전에는 아이폰과 아이패드의 스토리보드를 구분해서 개발했지만

  Adaptive Layout이 도입된 이 후 하나의 Universal Storyboard에서 개발한다.

  개발 입장에서 아이폰과 아이패드의 구분이 거의 없어졌다.

  Size Class를 통해 UI를 표시할 수 있는 영역의 크기를 큰 틀에서 구분하고,

  Trait Collection을 통해 상세한 인터페이스 환경을 구분하는 방식으로 변경되었다.

---

## springs and struts

오토 레이아웃을 사용하는 요즘은 Frame-Based Layout와 Autoresizing Mask를

사용하는 경우가 잘 없지만 여전히 활용가치가 있기에 알고 넘어가야하는 방식이다.

springs and struts는 Frame-Based Layout와 Autoresizing Mask를 통합해서 지칭한다.

<img width="953" alt="스크린샷 2021-02-11 오후 3 03 22" src="https://user-images.githubusercontent.com/70311145/107607185-daa5ac80-6c7b-11eb-9090-4fc2c4e22b1e.png">

스토리보드에 뷰를 올리고 오른쪽 인스펙터에서 x,y와 넓이 높이를 지정해주면

뷰의 프레임이 입력된 값으로 업데이트 된다.

springs and struts에서는 여기에서 입력한 프레임이 디자인 타임의 프레임인 동시에 런타임의 프레임이다.

인터페이스 빌더에서 뷰를 추가하고 아무런 제약도 추가하지 않으면 뷰의 프레임을 기반으로

제약을 자동으로 추가해준다. 이 제약을 **Prototyping Constraint**라고 한다.

만약 제약을 직접 추가한다면 사이즈 인스펙터에서 입력한 프레임 값은 디자인 타임의 프레임일 뿐

런타임 프레임은 아니다. 또한 Prototyping Constraint도 더 이상 추가되지 않는다.

- 오토 레이아웃에서 최종 프레임 값을 결정하는 요소는 오토 레이아웃이다. 프레임을 변경하고 싶다면 사이즈 인스펙터에서 프레임을 수정하는 것이 아니라 관련 된 제약을 수정해야 한다.

<img width="255" alt="스크린샷 2021-02-11 오후 3 22 08" src="https://user-images.githubusercontent.com/70311145/107607558-ecd41a80-6c7c-11eb-87d6-6136c5767ac2.png">

Autoresizing은 항목은 두개의 영역으로 구분되어 있다.

왼쪽 항목은 빨간색 선을 통해 Autoresizing Mask를 설정할 수 있다.

오른쪽 항목은 설정된 마스크에 따라서 뷰의 프레임이 어떻게 업데이트 되는지 미리보기를 지원한다.

왼쪽에 항목을 다시 보면 큰 네모 안에 작은 네모를 통해 선이 구분되어있다.

바깥에 있는 선들은 Top, Right, Bottom, Left의 여백을 설정할 수 있고, 실선으로 표시된 부분은

상위 뷰의 크기에 따라 여백의 크기가 자동으로 변경된다.

빨간색으로 선택된 부분은 fixed margin이라 부르고 실선으로 표시된 곳은 flexible margin이라고 부른다.

작은 네모안에 있는 두개의 선은 각각 너비와 높이를 나타낸다.

마스크가 선택되어 있지 않다면 고정된 크기로 표시되고, 선택이 되면 상위 뷰의 크기에 따라 자동으로 변경된다.

Autoresizing Mask는 비교적 단순한 UI를 구성할 때에 오토 레이아웃에 비해 시간을 절약할 수 있지만

UI가 복잡해질수록 원하는 결과를 얻기 어려워지고 코드를 통해 함께 구현해야한다.

요즘에는 많이 사용하지 않지만 UI Prototyping에 활용하기 좋은 도구이기에 배워두면 좋다.

오토레이아웃의 경우 중간에 UI가 변경된다면 새로운 제약을 추가하거나 수정하는 과정에서

제약 오류가 발생할 수 있고, 기존 제약을 모두 제거하고 다시 추가하는 것도 효율 적이지 않다.

이러한 경우에 UI구성이 어느정도 확장되기 전까지 Autoresizing Mask를 사용하면 좋다.

Autoresizing Mask는 확장된 제약이 추가되면 자동으로 무시되기 때문에 제약과 충돌하지 않으며

일일이 삭제해야 하는 경우도 덜어준다.

---

## Auto Layout

현재 루트뷰 안에 또 하나의 뷰가 있고, 이 오렌지 색상의 뷰는 아무런 제약도 없다.

현재 프레임을 기반으로 자동으로 제약이 추가된다. 이 제약을 프로토타이핑 제약이라고 한다.

<img width="304" alt="스크린샷 2021-02-11 오후 5 51 57" src="https://user-images.githubusercontent.com/70311145/107616673-e3a17880-6c91-11eb-937e-c3237f6ada24.png">

오른쪽 하단을 보면 다섯개의 팝업이 있다. 캔버스 메뉴라고도 한다.

<img width="157" alt="스크린샷 2021-02-11 오후 5 54 53" src="https://user-images.githubusercontent.com/70311145/107616925-4bf05a00-6c92-11eb-83aa-3b1289706755.png">

제약을 추가할 뷰를 선택한 후 팝업 중 Add New Constraints를 선택하면 제약을 추가할 수 있는 팝업이 표시된다.

제약에는 Top, Bottom, Leading, Trailing, Width, Height등을 설정할 수 있다.

<img width="273" alt="스크린샷 2021-02-11 오후 5 55 06" src="https://user-images.githubusercontent.com/70311145/107616929-4d218700-6c92-11eb-8a38-4d157aee96ac.png">

Top, Leading, Trailing, Height을 선택하고 제약을 추가하게되면 뷰 주위에 파란색 바가 표시된다.

<img width="264" alt="스크린샷 2021-02-11 오후 6 02 47" src="https://user-images.githubusercontent.com/70311145/107617494-5d863180-6c93-11eb-9773-1fa5812720ce.png">

제약을 추가하는 또 다른 방법으로는 제약을 추가할 뷰를 선택후 컨트롤 키를 누른상태에서

지정할 상대의 뷰에 드래그하면 제약을 추가할 팝업이 표시된다.

팝업이 표시된 상태에서 원하는 제약을 누르면 해당 제약이 추가되고 Shift 키를 누른 상태에서

클릭하면 두개 이상의 제약을 함께 추가할 수 있다.

option키를 누르면 기본값과 다른 제약 옵션이 표시된다.

<img width="390" alt="스크린샷 2021-02-11 오후 6 05 13" src="https://user-images.githubusercontent.com/70311145/107617705-bce44180-6c93-11eb-9bca-868cf958780a.png">

선택한 뷰 내부에 컨트롤 드래그를 하게되면 whdth, height를 설정할 수 있다.

<img width="379" alt="스크린샷 2021-02-11 오후 6 10 48" src="https://user-images.githubusercontent.com/70311145/107618175-7c38f800-6c94-11eb-96fe-237e5e999bb8.png">

위와 같이 인터페이스 빌더를 통해 제약을 추가하는 방법은 두가지가 있다.

1. 캔버스 메뉴를 통해 제약을 추가하기
2. 컨트롤 드래그 방식으로 제약을 추가하기

캔버스 메뉴를 통한 제약을 추가할 때에는 뷰의 여러개의 제약을 한번에 추가할 때 편리하다.

컨트롤 드래그 방식은 두 뷰 사이의 제약을 추가할 때 편리하다.

컨트롤 드래그 방식을 조금 더 알아보자!

오렌지 뷰에서 그린 뷰로 컨트롤 드래그 하면 두 뷰 사이에 추가할 수 있는 제약이 팝업으로 표시된다.

<img width="408" alt="스크린샷 2021-02-11 오후 6 15 52" src="https://user-images.githubusercontent.com/70311145/107618618-3466a080-6c95-11eb-93bf-5454bcf089de.png">

흰색 영역으로 컨트롤 드래그를 하면 씬의 전체 영역이 강조된다.

이것은 선택한 뷰와 씬의 최상위 뷰에 제약이 추가되는 것을 의미한다.

<img width="328" alt="스크린샷 2021-02-11 오후 6 18 29" src="https://user-images.githubusercontent.com/70311145/107618840-91faed00-6c95-11eb-8bc3-4bf8ecd088c3.png">

> 컨트롤 드래그 방식에서는 드래그의 방향에 따라 추가할 수 있는 제약이 달라진다.

컨트롤 드래그 방식의 제약추가는 캔버스 내에서 뿐만 아니라 Document Outline에서도

제약을 추가할 수 있다. 이 방식에서는 드래그의 방향과 상관없이 두 뷰 사이의 모든 제약이 표시된다.

<img width="398" alt="스크린샷 2021-02-11 오후 6 21 39" src="https://user-images.githubusercontent.com/70311145/107619105-ffa71900-6c95-11eb-88ce-1ed80648a7ee.png">

컨트롤 드래그 방식은 뷰의 현재 프레임을 기준으로 제약이 추가되므로 미리 원하는 값으로 프레임을 설정해야한다.

하지만 컨버스 메뉴에서 제약을 추가할 경우에는 현재 프레임을 무시하고 제약을 추가할 수 있다.

Add New Constraints 팝업에서 width와 height를 추가해주면 프레임이 변경된다.

뷰의 테두리를 보면 빨간색으로 바가 표시되는데 오토레이아웃에서 빨간색 선은 오류를 나타낸다.

지금은 넓이와 높이면 설정되어있고 위치는 설정되어있지 않아 오류가 난 것이다.

<img width="742" alt="스크린샷 2021-02-11 오후 6 28 09" src="https://user-images.githubusercontent.com/70311145/107619728-f36f8b80-6c96-11eb-9203-f367b64da855.png">

Add New Alignment Constraints에서 제약을 추가하거나

Add New Constraints에서 네방향의 제약을 추가해주면 오류가 사라진다.

<img width="730" alt="스크린샷 2021-02-11 오후 6 28 23" src="https://user-images.githubusercontent.com/70311145/107619738-f7031280-6c96-11eb-9a2b-0e620b9b6ac7.png">

뷰에서의 제약이 걸린 바를 선택하게 되면 강조가 되어서 표시된다.

바의 명칭은 애플 공식문서에서는 IBar로 불리고 있다.

IBar는 공간의 크기 또는 너비 높이와 관련된 제약을 표현한다.

<img width="313" alt="스크린샷 2021-02-11 오후 6 35 12" src="https://user-images.githubusercontent.com/70311145/107620361-e7d09480-6c97-11eb-9440-6149475a63d7.png">

원하는 IBar를 선택하고 오른쪽 인스펙터를 보면 다양한 옵션을 변경할 수 있다.

<img width="258" alt="스크린샷 2021-02-11 오후 6 35 16" src="https://user-images.githubusercontent.com/70311145/107620364-e901c180-6c97-11eb-9e21-a017f3e3d07d.png">

제약이 추가된 상태에서 뷰를 옮기게 되면 비쥬얼 인디케이터가 주황색으로 표시된다.

이 것은 제약에는 오류가 없지만 현재 프레임과 계산된 최종 프레임이 다르다는 것을 나타낸다.

최종 프레임은 주황색 점선으로 표시되고, 실선 위에 두개의 프레임 차이가 표시된다.

<img width="318" alt="스크린샷 2021-02-11 오후 6 40 36" src="https://user-images.githubusercontent.com/70311145/107620849-b5736700-6c98-11eb-8b40-07d36467e820.png">

위 같은 경우에 캔버스 메뉴의 첫번째 버튼을 눌러주면 최종 프레임으로 이동시켜 준다.

<img width="31" alt="스크린샷 2021-02-11 오후 6 40 59" src="https://user-images.githubusercontent.com/70311145/107620851-b73d2a80-6c98-11eb-99e6-5e85ebfdf5a8.png">

제약에 오류가 있으면 Document Outline에서 빨간색으로 화살표가 표시되고

클릭하게 되면 오류에 대한 상세한 정보를 얻을 수 있다.

<img width="822" alt="스크린샷 2021-02-11 오후 6 45 48" src="https://user-images.githubusercontent.com/70311145/107621339-71349680-6c99-11eb-9bf8-ddbe68b5f565.png">

화살표를 눌러 상세 오류를 보게되면 오른 쪽에 빨간색으로 아이콘이 표시되는데

Add Missing Constraints를 눌러 필요한 재약을 자동으로 표시할 수 있다.

하지만 자동으로 추가된 제약이 필요한 제약과 다를 수 있어서 가능한 직접 추가하는 것이 좋다.

<img width="552" alt="스크린샷 2021-02-11 오후 6 46 05" src="https://user-images.githubusercontent.com/70311145/107621349-742f8700-6c99-11eb-880b-59569f4e2c7c.png">

가로 정렬을 나타내는 실선을 선택후 오른 쪽의 인스펙터를 보면 Priority가 1000으로 되어있다.

우선순위 1000은 필수 제약을 의미하고, 필수제약은 항상 실선으로 표시한다.

<img width="859" alt="스크린샷 2021-02-11 오후 6 54 33" src="https://user-images.githubusercontent.com/70311145/107622081-aab9d180-6c9a-11eb-98e1-7fb4f146af74.png">

우선순위인 1000보다 작은 값을 설정하면 실선이 점선으로 표시된다.

우선순위가 1000보다 작은 제약은 모두 선택적 제약이 되고, 우선 순위에 상관없이 항상 점선으로 표시된다.

<img width="862" alt="스크린샷 2021-02-11 오후 6 57 42" src="https://user-images.githubusercontent.com/70311145/107622318-08e6b480-6c9b-11eb-8f5a-318f8e2f06a8.png">

---

Document Outline을 보면 뷰와 연관된 제약이 표시된다.

제약의 종류에 따라서 추가되는 위치가 달라진다.

<img width="268" alt="스크린샷 2021-02-11 오후 11 23 54" src="https://user-images.githubusercontent.com/70311145/107648916-3d209c00-6cc0-11eb-9685-1d41a358d635.png">

다른 뷰와의 연관성이 없는 width, height 제약은 해당 뷰의 바로 아래 추가되고,

다른 뷰와 연관된 제약들은 연관된 뷰들이 포함되어있는 최상위 뷰 중에서 가장 인접한 상위 뷰 아랫쪽에 추가된다.

leading, trailing, top, bottom, centerX, centerY 등의 제약은

모두 상위 뷰와의 관계를 나타내는 제약이다. 그래서 선택된 뷰 아랫쪽에 표시되는 것이 아니라

인접한 상위뷰인 루트뷰 아랫쪽에 추가된다.

Document Outline에서 제약을 선택하면 캔버스에서 해당 제약이 선택되고,

속성 인스펙터와 사이즈 인스펙터에서 제약의 속성을 변경할 수 있다. 제약은 이름은 개요로 표시된다.

<img width="269" alt="스크린샷 2021-02-11 오후 11 36 10" src="https://user-images.githubusercontent.com/70311145/107650546-f03dc500-6cc1-11eb-8ba6-ea2ac7b68654.png">

씬에서 제약이 추가된 뷰를 선택하고 사이즈 인스펙터에 Constraints 속성을 보면

뷰에 추가되어있는 제약 목록이 표시된다. 상단에 미리보기에서의 파란색 선은

추가되어있는 제약을 나타내는데 선을 클릭하면 필터링 목록이 토글된다.

미리보리 아래에 목록들에 마우스를 올리면 해당 제약이 캔버스에서 강조되고

클릭하면 선택이 된다. 오른쪽에 Edit를 클릭하면 주요한 속성을 변경할 수 있는 팝업이 표시된다.

<img width="259" alt="스크린샷 2021-02-11 오후 11 38 07" src="https://user-images.githubusercontent.com/70311145/107650827-35fa8d80-6cc2-11eb-8192-ca56a73033fb.png">

---

스토리보드로 UI를 구성할 때에는 미리보기를 제공한다.

디자인을 하나하나 변경할 때마다 앱을 실행해서 확인하는 수고를 덜어주는 장점이 있다.

<img width="57" alt="스크린샷 2021-02-11 오후 11 45 25" src="https://user-images.githubusercontent.com/70311145/107651764-3b0c0c80-6cc3-11eb-8485-0a3d691f7398.png">

오른쪽 상단에 Adjust Editor on Right을 클릭하여 Preview를 클릭하면

적용한 오토레이아웃을 바로 확인해 볼 수 있고 다양한 디바이스를 추가해서 확인이 가능하며

가로, 세로 모드에의 오토레이아웃 적용도 바로바로 확인 할 수 있다.

<img width="1154" alt="스크린샷 2021-02-11 오후 11 45 56" src="https://user-images.githubusercontent.com/70311145/107651832-4c551900-6cc3-11eb-868c-993491b8eca9.png">

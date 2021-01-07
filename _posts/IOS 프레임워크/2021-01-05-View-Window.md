---
title:  "iOS) view & window"
excerpt: "코코아 터치 프레임워크와 UIKit"
header:


categories:
  - ios
tags:
  - ios
  - uikit
last_modified_at: 2019-04-13T08:06:00-05:00
---
# view & window

모든 앱은 적어도 하나의 window를 가지고있다.

window는 눈에 보이지 않는 요소이지만 중요한 역할을 수행한다.

터치 이벤트를 올바른 대상으로 전달해주고, 화면에 표시되는 view에 컨테이너 역할을 한다.

view는 반드시 window에 추가되어 작업해야한다.

앱에서 시각적으로 표시되는 부분은 모드 view로 표현한다.

view는 다음 세가지 역할을 하게된다.

1. 화면의 content 출력
2. 터치이벤트를 처리
3. subView의 배치를 관리

코코아 터치 프레임워크는 다양한 System view들을 제공한다.

---

### 코코아 터치 프레임워크란??    

~~코코아는 먹는거 밖에 모르는😂~~

코코아 프레임워크를 알기전에 먼저 프레임워크가 뭔지 알아야겠지??

Framework는 해석하면 뼈대이다.

라이브러리는 클래스와 완성되어있는 메서드들을 미리 만들어놓고 필요할때마다 뽑아서 쓰는거라면

프레임워크는 미완성 된 클래스와 메서드들을 개발자가 뼈대에 살을 붙이듯 앱을 개발할 때 편리하고 빠르게

구현할 수 있도록 진짜 뼈대만 세워두는 것이다.

저러한 프레임워크들을 여러개 모아서 더욱 큰 프레임워크를 구성한 것이 코코아 프레임워크이다!!

그럼 코코아 터치 프레임워크가 무엇이냐면 코코아 프레임워크 내에서 **터치** 와 관련된 디바이스의 앱을 개발할 때

사용하는 도구이다. 보통 ios개발을 할 때 이 코코아 터치 프레임워크를 사용하게 된다.

공부하면서 보았던 맨 위에 **import**로 불러오는 것들이 저기에 해당된다.

```swift
import UIKit
import Foundation
```

등등,,

-----

다시 System view로 돌아와보자.

system view는 다섯개의 카테고리로 분류할 수 있다.

Text Views

- Label
- Text Field (싱글라인)
- Text View (멀티라인)

Controls

- Button
- Switch
- Slider
- Page Control
- Date Picker
- Segmented Control
- Stepper

Content Views

- Image VIew
- Picker VIew
- Progress View
- Activity Indecator View
- Web View
- Map View

Container Views

- Scroll View
- Table View
- Collection View
- Stack View

Bars

- Navigation Bar
- Tab Bar
- Tool Bar
- Search Bar

이러한 system view들은 **UIKit Framework** 를 통해 제공한다. 지정되어있는 이름들이 직관적이라서

각각 어떠한 기능을 하는지 알아보기쉬울 것 같다!!

<img width="1007" alt="viewWindow" src="https://user-images.githubusercontent.com/70311145/103649890-8afc0300-4fa2-11eb-85f8-7d83b11ab5bf.png">

UIView가 제공되어있고 모두 이 클래스를 상속받고 있다. *(KXCoding 강의에서 image를 사용하였습니다. )*

# UIKit) Date Picker & Date Formatter

## DatePicker

> ios reference -> [UIDatePicker](https://developer.apple.com/documentation/uikit/uidatepicker)

ios에서 날짜를 선택하는 대부분의 UI는 DatePicker를 통해 구현한다.

유사한 UI를 가진 Picker View와 달리 Date를 표시하는 코드를 직접 구현할 필요가 없다.

선택 이벤트를 처리할 때는 Target-Action 메커니즘을 사용한다.

```swift
class UIPickerView: UIControl
```

UIControl을 상속받고 있는 클래스 이기 때문!!

---

DatePicker를 한번 사용해보도록 하자! 라이브러리를 키고 인터페이스빌더에 드래그해준다.

<img width="682" alt="스크린샷 2021-01-13 오후 5 22 05" src="https://user-images.githubusercontent.com/70311145/104425782-6e745200-55c4-11eb-9ade-bee63afa4901.png">

특별한 이유가 없다면 너비는 인터페이스 너비에 맞추고, 높이는 현재 높이로 설정한다.

<img width="266" alt="스크린샷 2021-01-13 오후 5 24 42" src="https://user-images.githubusercontent.com/70311145/104425796-7207d900-55c4-11eb-8bc0-66e47fe572f0.png">

오토레이아웃을 위 왼쪽 오른쪽에 제약을 주고 높이를 현재값으로 설정했다.

<img width="425" alt="스크린샷 2021-01-13 오후 5 27 53" src="https://user-images.githubusercontent.com/70311145/104426017-b8f5ce80-55c4-11eb-8b9e-25898615c5ed.png">

Date Picker의 속성들을 알아보자.

<img width="256" alt="스크린샷 2021-01-13 오후 5 25 52" src="https://user-images.githubusercontent.com/70311145/104425799-73390600-55c4-11eb-9046-80e66fdefbb8.png">

Mode - 기본적으로 날짜와 시간을 동시에 선택할 수 있다.

- Time - 시간을 개별적으로 선택할 수 있다.
- Date - 날짜를 개별적으로 선택할 수 있다.
- Count Down Timer - 말 그대로 count down

Locale - 지역을 설정 (나라)

Interval - Date Picker가 분을 표시해야하는 간격.

preferred Style - DatePicker의 스타일을 지정.

데이터피커를 아웃렛으로 연결해주고 속성들을 viewDidLoad에서 코드로 적용해보았다.

<img width="685" alt="스크린샷 2021-01-13 오후 6 41 20" src="https://user-images.githubusercontent.com/70311145/104434769-f6f7f000-55ce-11eb-9542-73c77e4bced2.png">

![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/70311145/104435156-67067600-55cf-11eb-8f57-407d83951012.gif)

지금 콘솔에 출력되는 부분은 실제 앱을 만들때 문자열로 표시해야 한다.

그 부분은 Date Formatter를 통해서 문자열로 바꿔야 한다.

---

## Date Formatter

날짜를 원하는 형식의 문자열로 바꿀때 사용되는 것이 Date Formatter이다.

새로운 인스턴스를 만들고, 출력할 문자열의 형식을 지정하면 된다.

```swift
let formatter = DateFormatter()
```

그런 다음 String 또는 localized String으로 시작하는 메서드로 날짜를 전달한다.

형식을 지정할 때에는 미리 지정된 형식을 사용하거나 직접 포맷 문자열을 설정할 수 있다.

미리 지정된 형식을 사용할 때에는 날짜와 시간 형식을 별도로 설정해야한다.

```swift
// 날짜 형식은 dateStyle로 설정
formatter.dateStyle = .full

// 시간 형식은 timeStyle로 설정
formatter.timeStyle = .medium
```

스타일의 종류는 다섯가지 이다.

> .full .long .medium .short .none

.none을 사용하면 해당 파트가 문자열에 포함되지 않는다.

두 속성 모두 none이 기본값이기 때문에 반드시 둘 중하나는 none이 아닌 값으로 설정해야한다.

| Date   | Time   | Date / Time String                                             |
| ------ | ------ | -------------------------------------------------------------- |
| none   | none   |                                                                |
| none   | short  | 7:42 PM                                                        |
| none   | medium | 7:42:24 PM                                                     |
| none   | long   | 7:42:24 PM GMT+9                                               |
| none   | full   | 7:42:24 PM Korean Standard Time                                |
| short  | none   | 1/13/21                                                        |
| short  | short  | 1/13/21, 7:42 PM                                               |
| short  | medium | 1/13/21, 7:42:24 PM                                            |
| short  | long   | 1/13/21, 7:42:24 PM GMT+9                                      |
| short  | full   | 1/13/21, 7:42:24 PM Korean Standard Time                       |
| medium | none   | Jan 13, 2021                                                   |
| medium | short  | Jan 13, 2021 at 7:42 PM                                        |
| medium | medium | Jan 13, 2021 at 7:42:24 PM                                     |
| medium | long   | Jan 13, 2021 at 7:42:24 PM GMT+9                               |
| medium | full   | Jan 13, 2021 at 7:42:24 PM Korean Standard Time                |
| long   | none   | January 13, 2021                                               |
| long   | short  | January 13, 2021 at 7:42 PM                                    |
| long   | medium | January 13, 2021 at 7:42:24 PM                                 |
| long   | long   | January 13, 2021 at 7:42:24 PM GMT+9                           |
| long   | full   | January 13, 2021 at 7:42:24 PM Korean Standard Time            |
| full   | none   | Wednesday, January 13, 2021                                    |
| full   | short  | Wednesday, January 13, 2021 at 7:42 PM                         |
| full   | medium | Wednesday, January 13, 2021 at 7:42:24 PM                      |
| full   | long   | Wednesday, January 13, 2021 at 7:42:24 PM GMT+9                |
| full   | full   | Wednesday, January 13, 2021 at 7:42:24 PM Korean Standard Time |

위의 표는 string(from:)메서드를 통해 출력한 값을 나타낸 것이다.

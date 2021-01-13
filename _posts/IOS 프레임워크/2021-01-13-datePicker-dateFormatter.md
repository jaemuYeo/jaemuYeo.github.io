---
title: "UIKit) Date Picker & Date Formatter"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-14

last_modified_at: 2021-01-14
---

# Date Picker와 Date Formatter 알아보기.

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

그런 다음 String 또는 localizedString으로 시작하는 메서드로 날짜를 전달한다.

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

```swift
let now = Date() // 현재시간을 나타냄

let formatter = DateFormatter()

formatter.dateStyle = .full // dateStyle 을 full로 지정
formatter.timeStyle = .medium // timeStyle 을 medium으로 지정

var result = formatter.string(frome: now)
print(result) // Wednesday, January 13, 2021 at 7:42:24 PM

formatter.string(for: now)
```

위 코드는 현재의 시간을 문자열로 나타낸 코드이다.

파라미터로 전달하는 문자가 옵셔널이라면 string(for:) 메서드를 사용할 수 있다.

한국어로 출력을 하고싶으면 locale을 사용하면 된다.

```swift
formatter.locale = Locale(identifier: "ko_KR")
// 2021년 1월 13일 수요일 오후 7시 42분 24초 대한민국 표준시
```

Formatter를 반복적으로 사용하지 않는다면 위에 코드처럼 인스턴스를 생성하지 않고

클래스함수를 사용할 수 있다.

```swift
DateFormatter.localizedString(from: now, dateStyle: .long, timeStyle: .short)
```

formatter 문자열을 통해 지역화된 문자열을 얻을 때에는

setLocalizedDateFormatFromTemplate(dateFormatTemlpate:String) 메서드를 사용한다.

Date를 String로 표현하기 위해서는 YYYYMMDD 같은 locale identifier을 알고있어야한다.

**[한국과 미국을 표준으로 한 표를 참고하였다](https://popopo.tistory.com/156)**

- a: am/pm -> Locale(identifier: "ko") 같이 한국으로 설정해주면 오전/오후로 표시
- e: 요일 -> e의 갯수에따라서 월, 월요일, 주간요일순서를 숫자로 표현
- y: 년
- M: 월
- d: 일
- D: 365일 중 day를 나타냄
- H: 시(24시표현)
- h: 12시형식
- m: 분
- s: 초

'-'나 공백도 맞춰서 똑같이 표현해야한다.

패턴의 예를 간단하게 들어보자

yyyy.MM.dd -> 2021.01.13

yyyy@ HH : mm -> 2021@ 17 : 42

이렇게 DateFormatter를 잘 이용하면 원하는 날짜 형식으로 표현이 가능하다.

```swift
let now = Date()
let formatter = DateFormatter()
// 년, 월, 일, 요일이 포함된 포멧문자열 생성
formatter.setLocalizedDateFormatFromTemplate("yyyyMMMMdE")

// 영어 locale 설정
formatter.locale = Locale(identifier: "en_US")
var result = formatter.string(from: now)
print(result) // Wed, January 13, 2021

// 한국 locale 설정
formatter.locale = Locale(identifier: "ko_KR")
result = formatter.string(from: now)
print(result) //수, 1월 13, 2021
```

위 코드를 보면 한국 locale 부분에서 이상함이 느껴진다.

한글로 출력은 되지만 미국형식과 동일하다. 그 이유는 dateFormat이 locale에 맞게

업데이트 되지 않아서 그렇다. locale을 바꾼다 해서 Fromat문자열이 자동으로

업데이트 되지는 않는다. 그래서 locale을 바꾸고 나서 메서드를 다시 호출해야한다.

```swift
let now = Date()
let formatter = DateFormatter()

formatter.locale = Locale(identifier: "en_US")
formatter.setLocalizedDateFormatFromTemplate("yyyyMMMMdE")
var result = formatter.string(from: now)
print(result) // Wed, January 13, 2021

formatter.locale = Locale(identifier: "ko_KR")
formatter.setLocalizedDateFormatFromTemplate("yyyyMMMMdE")
result = formatter.string(from: now)
print(result) // 2021년 1월 13일 (수)
```

이제는 locale에 적합한 문자열이 출력된 것을 볼 수 있다!!

직접 원하는 Format을 설정할 수도 있다.

```swift
formatter.dateFormat = "yyyyMMMMde"
result = formatter.string(from: now)
print(result) //20211월134
```

이렇게 하면 Format문자로 지정한 Format과 순서가 그대로 반영된 문자열이 출력된다.

이 방식은 locale에 관계없이 고정된 Format이 필요할 때 주로 사용된다.

날짜는 기본적으로 년,월,일로 표시되지만 현재시점을 기준으로 상대적으로 표현도 가능하다.

```swift
import Foundation

let now = Date()
let yesterday = now.addingTimeInterval(3600 * -24)
let tomorrow = now.addingTimeInterval(3600 * 24)

let formatter = DateFormatter()
formatter.locale = Locale(identifier: "ko_KR")
formatter.dateStyle = .full
formatter.timeStyle = .none

formatter.doesRelativeDateFormatting = true

print(formatter.string(from: now)) // 어제
print(formatter.string(from: yesterday)) // 오늘
print(formatter.string(from: tomorrow)) // 내일

```

doesRelativeDateFormatting 속성을 사용하면 48시간 이내의 날짜를

그저께, 어제, 오늘, 내일, 모레와같은 상대적인 문자열로 바꿀 수 있다.

Symbol을 통해 이모티콘을 요일과 오전,오후로 표현도 가능하다.

```swift
let now = Date()
let weekdaySymbols = ["❤️", "🧡", "💛", "💚", "💙", "💜", "🤍"]
let am = "🌞"
let pm = "🌙"

let formatter = DateFormatter()
formatter.dateStyle = .full
formatter.timeStyle = .full

print(formatter.string(from: now))
// Thursday, January 14, 2021 at 12:44:49 AM Korean Standard Time

formatter.amSymbol = am
formatter.pmSymbol = pm

formatter.weekdaySymbols = weekdaySymbols

print(formatter.string(from: now))
// 💙, January 14, 2021 at 12:44:49 🌞 Korean Standard Time
```

Date를 String으로 바꾸어보았다면 String을 Date로 파싱하는 법도 있다.

문자열을 날짜로 바꿀때에는 dateFormat속성을 통해 날짜 format을 정확히 지정해야한다.

```swift
let str = "2021-01-014T01:30:00Z"
let formatter = DateFormatter()
// 문자열과 동일한 포맷을 지정
formatter.dateFormat = "yyyy-MM-dd'T'HH:mm:ss'Z'"

if let date = formatter.date(from: str) {
    // 파싱에 성공하면 style을 .full 로 설정
    formatter.dateStyle = .full
    formatter.timeStyle = .full
    print(formatter.string(from: date))
} else {
    print("유효하지 않음")
}

// Thursday, January 14, 2021 at 1:30:00 AM Korean Standard Time
```

date(from:)메서드는 성공한경우 날짜를 리턴하고 실패하면 nil을 리턴한다.

그러므로 대부분 옵셔널 바인딩 형식으로 처리한다.

T와 Z 같은 구분문자를 '' 로 감싸줘야한다.

날짜 문자에 포함된 구분문자는 작은따음표로 감싸서 dateFormat패턴 문자와 구분해야한다.

이와 같은 방식을 사용할 때는 dateFormat속성을 정확히 지정해야 한다.

조금이라도 오타가 생기면 파싱에 실패하게 되므로 주의해야한다.

---

## Count Down Timer

위에서 보았던 datePicker의 모드 중 Count Down Timer를 구현해보자.

<img width="322" alt="스크린샷 2021-01-14 오전 2 02 51" src="https://user-images.githubusercontent.com/70311145/104484421-a1dacf00-560c-11eb-934a-9c34c536e41d.png">

datePicker에서 시간과 분을 설정한뒤 버튼을 누르면 카운트다운을

실행하는 간단한 앱을 구현할 것이다.

<img width="510" alt="스크린샷 2021-01-14 오전 2 04 10" src="https://user-images.githubusercontent.com/70311145/104484606-cfc01380-560c-11eb-99c8-067b95973748.png">

Label과 datePicker를 아웃렛에 연결하고 Button을 액션으로 연결하였다.

Count Down Timer에서 선택할 수 있는 가장 작은 설정값은 1분이다.

그리고 선택할 수 있는 가장 큰 값은 23시간 59분이다.

<img width="341" alt="스크린샷 2021-01-14 오전 2 32 33" src="https://user-images.githubusercontent.com/70311145/104487769-dc466b00-5610-11eb-8f85-0b6a695c5c3e.png">

Count Down Timer는 이름과 달리 카운트 다운을 직접 처리하지 못한다.

이 부분은 타이머를 활용해서 직접 구현해야 한다.

<img width="420" alt="스크린샷 2021-01-14 오전 2 33 51" src="https://user-images.githubusercontent.com/70311145/104487850-f41def00-5610-11eb-8496-771e34ddfe5a.png">

남은 시간을 저장할 속성을 선언하고 0으로 초기화 한다.

<img width="629" alt="스크린샷 2021-01-14 오전 2 34 47" src="https://user-images.githubusercontent.com/70311145/104487979-1b74bc00-5611-11eb-94ed-fa5ebe936ea4.png">

Timer가 제공하는 메서드를 통해 반복할 코드를 구현한다.

첫번째 파라미터는 반복주기를 전달하고

두번째 파라미터에 false가 적용되면 한번만 실행되고 타이머가 종료된다.

세번째 파라미터에는 실행할 코드를 전달한다.

남은 시간을 1초씩 줄이고 Label을 업데이트한다.

<img width="326" alt="스크린샷 2021-01-14 오전 2 37 03" src="https://user-images.githubusercontent.com/70311145/104488221-67bffc00-5611-11eb-8ffe-1b8cecc29368.png">

마지막으로 남은 시간이 0이면 타이머가 종료하고 기본효과음을 재생한다.

**전체코드**

<img width="707" alt="스크린샷 2021-01-14 오전 2 37 53" src="https://user-images.githubusercontent.com/70311145/104488310-845c3400-5611-11eb-8a28-fd859066702d.png">

**앱 실행**

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/104488568-e3ba4400-5611-11eb-8ac9-0049e2680fb3.gif)

---
title: "UIKit) Text Delegates"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-16

last_modified_at: 2021-01-16
---

# Text Field Delegate & Text View Delegate 배워보기.

공식 문서

- [UITextFieldDelegate](https://developer.apple.com/documentation/uikit/uitextfielddelegate)
- [UITextViewDelegate](https://developer.apple.com/documentation/uikit/uitextviewdelegate)

텍스트 필드와 텍스트뷰는 델리게이트패턴을 통해 이벤트를 처리한다.

이벤트 처리에 사용되는 메서드는 각각의 프로토콜에 선언되어있다.

앞에서 배웠던 두 텍스트 처리패턴이 비슷한것 처럼 두 프로토콜에 선언되어있는

메서드와 호출 시점도 유사하다.

텍스트 필드와 텍스트 뷰를 탭하게 되면

> Tap -> First Responder 호출 -> Editing Session 전환

First Responder가 호출 되고 편집모드로 전환된다. 그리고 키보드가 나타난다.

더 상세히 알아보면 Tap 시점에 델리게이트 메서드가 호출되고 여기서 True를 리턴하면

First Responder가 된다.

```swift
textFieldShouldBeginEditing(_:)
textViewShouldBeginEditing(_:)
```

이 메서드를 구현하지 않으면 True를 리턴하는 것과 비슷하다.

편집모드가 시작된 직후에는

```swift
textFieldDidBeginEditing(_:)
textViewDidBeginEditing(_:)
```

이 메서드가 실행되고, 이 후 텍스트를 입력하거나 삭제하면

연관된 델리게이트 메서드가 반복적으로 호출하게 된다.

```swift
// 입력 할 수 있는 길이를 제한하거나 특정 문자의 입력을 금지
textField(_:shouldChangeCharactersIn:replacementString:)
// 메서드와 파라미터이름은 다르지만 textField와 동일한 기능 구현
textVIew(_:shouldChangeTextIn:replacementText:)
```

위 의 코드가 실행되고나서 각각의 메서드가 호출된다.

```swift
// 삭제버튼을 클릭 했을 때 실행
textFieldShouldClear(_:)
// 사용자가 직접 편집을 했을 때 연달아 실행
textViewDidChange(_:)
```

메서드 이름에 should 가 포함되어있다면 Bool값을 리턴해야 한다.

textFieldShouldClear(\_:)메서드에 True를 리턴하면 입력된 값을 삭제한다.

```swift
// textField에서 리턴키를 탭했을때 호출
textFieldShouldReturn(_:)
// textView에서 특정법위를 선택하거나 입력포인트를 이동시킬 때 호출
textViewDidChangeSelection(_:)
```

textVIew는 attachment객체를 통해서 이미지를 텍스트와 함께 출력 할 수 있다.

또는 Date detector를 통해 해당 속성에 맞게 인식할 수 있다.

```swift

textView(_:shouldInteractWith:in:interaction:)
```

이런 객체들을 터치할 때 호출 되는 메서드가 textView(\_:shouldInteractWith:in:interaction:)이다.

편집모드가 종료되기 직전에는 밑에 두 메서드가 호출된다.

```swift
textFieldShouldEndEditing(_:)
textViewShouldEndEditing(_:)
```

위의 메서드에서 True를 리턴하게 되면 편집모드가 종료하게 되고

키보드가 화면에서 사라진다. (false를 입력하면 입력포커스 그대로 유지!)

편집모드가 종료된 직후에는 밑에 두 메서드가 호출된다.

```swift
textFieldDidEndEditing(_:)
textCiewDidEndEditing(_:)
```

여기까지해서 두 Text개체의 델리게이트가 구현되는 과정을 알아보았다.

정말 textField와 textView의 델리게이트가 유사한 패턴을 가진것을 느낄 수 있다!!

첫번 째 파라미터에는 항상 메서드를 호출한 뷰가 전달된다.

하나의 씬에 여러개의 textFiedl와 textView가 추가되어있고 델리게이트가 동일한 객체로 저장되어 있는 경우

첫번 째 파라미터를 통해 코드를 분기할 수 있다.

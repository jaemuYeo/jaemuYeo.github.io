---

title: "UIControl & Target-Action 1" 

categories:

 - ios

tags:

 - [UIKit,framework]



toc: true

toc_sticky: true



date: 2021-01-07

last_modified_at: 2021-01-07

---

# UIControl & Target-Action ?

저번시간에 코코아 터치 프레임워크가 무엇이고 이미지를 통해 UIKit의 구조를 보았다.

UIKit프레임워크에 속해있는 UIControl에 대해서 오늘은 알아보자.

<img width="1015" alt="스크린샷 2021-01-07 오후 7 29 58" src="https://user-images.githubusercontent.com/70311145/103882366-084c8280-511f-11eb-97cc-417d2798a1f4.png">

- Button
- Switch
- Slider
- Page Control
- Date Picker
- Segmented Control
- Stepper

위에 있는 것들이 **UIControl**에 구현되어있다.

UIControl 클래스는 UIView 클래스를 상속하고 나열되어있는 클래스들은

UIControl클래스를 상속하고있다.

그래서 예를들어 Button이면 UIButton, Switch이면 UISwitch 처럼 UI라는 접두어가 붙는다!!

나중에 다른 UIView클래스를 알아볼때도 이어질 내용이니 기억하도록~



### Target-Action

컨트롤은 다양한 상태를 가지고있고, 자신의 상태를 시각적으로 표현한다.

그리고 터치의 종류에 따라서 다양한 이벤트를 제공한다.

컨트롤이 전달하는 이벤트는 Target-Action 메커니즘으로 처리한다.

> **이벤트처리??**
>
> iOS 개발에서는 컨트롤과 코드를 연결하고 이벤트를 처리한다.
>
> 이러한 것을 Target-Action메커니즘 또는 Target-Action패턴이라고 부른다.

간단하게 말하자면 버튼을 씬에 추가하고 액션으로 연걸하는것.

[코드](https://developer.apple.com/documentation/uikit/uicontrol/1618259-addtarget)에서 타깃과 액션을 구현할 때에는 

```swift
func addTarget(Any?, action: Selector, for: UIControl.Event)
```

메서드를 사용한다.

Action은 이벤트가 발생하면 호출되는  메서드이고,

Target은 이 메서드가 구현되어있는 객체이다.

Selector은 Objective-C에서 사용하던 개념이고 그냥 메서드라고 생각해도 된다.

메서드를 Selector로 바꾸는 코드는 밑의 내용에서 알아보도록 하겠다.

Event는 [공식문서](https://developer.apple.com/documentation/uikit/uicontrol/event)에서 보면 많은 이벤트 들이있지만 주로 사용하는 것은

**touchUpInside**와 **valueChanged** 이다.

|UIControl.Event||
|---|---|
|touchDown|컨트롤을 터치했을 때 발생하는 이벤트|
|touchDownRepeat|컨트롤을 연속 터치 할 때 발생하는 이벤트|
|touchDragInside|컨트롤 범위 내에서 터치한 영역을 드래그 할 때 발생하는 이벤트
|touchDragOutside|터치 영역이 컨트롤의 바깥쪽에서 드래그 할 때 발생하는 이벤트
|touchDragEnter|터치 영역이 컨트롤의 일정 영역 바깥쪽으로 나갔다가 다시 들어왔을 때 발생하는 이벤트
|touchDragExit|터치 영역이 컨트롤의 일정 영역 바깥쪽으로 나갔을 때 발생하는 이벤트
|touchUpInside|컨트롤 영역 안쪽에서 터치 후 뗐을때 발생하는 이벤트
|touchUpOutside|컨트롤 영역 안쪽에서 터치 후 컨트롤 밖에서 뗐을때 이벤트
|touchCancel|터치를 취소하는 이벤트 (touchUp 이벤트가 발생되지 않음)
|valueChanged|터치를 드래그 및 다른 방법으로 조작하여 값이 변경되었을때 발생하는 이벤트
|primaryActionTriggered|버튼이 눌릴때 발생하는 이벤트 (iOS보다는 tvOS에서 사용)
|editingDidBegin|UITextField에서 편집이 시작될 때 호출되는 이벤트
|editingChanged|UITextField에서 값이 바뀔 때마다 호출되는 이벤트
|editingDidEnd|UITextField에서 외부객체와의 상호작용으로 인해 편집이 종료되었을 때 발생하는 이벤트
|editingDidEndOnExit|UITextField의 편집상태에서 키보드의 return 키를 터치했을 때 발생하는 이벤트
|allTouchEvents|모든 터치 이벤트
|allEditingEvents|UITextField에서 편집작업의 이벤트
|applicationReserved|각각의 애플리케이션에서 프로그래머가 임의로 지정할 수 있는 이벤트 값의 범위
|systemReserved|프레임워크 내에서 사용하는 예약된 이벤트 값의 범위
|allEvents|시스템 이벤트를 포함한 모든 이벤트



<img width="480" alt="스크린샷 2021-01-07 오후 8 03 44" src="https://user-images.githubusercontent.com/70311145/103885516-7c892500-5123-11eb-95c6-1704257eb251.png">

인터페이스 빌더를 통해 Action 메서드를 구현할 수 있는 코드는 이렇게 세가지가 있고 인자값을 제외한 동일한 코드이다.

인터페이스 빌더로 Action메서드를 구현할 때에는 **@IBAction** 이 붙어야 한다.

<img width="247" alt="스크린샷 2021-01-07 오후 8 08 28" src="https://user-images.githubusercontent.com/70311145/103886104-57e17d00-5124-11eb-8791-5ed2e8562c61.png">

<img width="251" alt="스크린샷 2021-01-07 오후 8 09 38" src="https://user-images.githubusercontent.com/70311145/103886145-6891f300-5124-11eb-9876-0e1c5a9992f5.png">

위의 그림의 Event를 보면 첫번째는 Slider 두번째는 Button인데 각각 기능에 맞게끔 Event를 자동으로 지정해준다!!

이번에는 코드를 통해서 Action을 연결해보자.

<img width="516" alt="스크린샷 2021-01-07 오후 8 18 21" src="https://user-images.githubusercontent.com/70311145/103886894-8875e680-5125-11eb-9d4e-1215a5d472fe.png">

Button을 @IBOutlet으로 선언하고 메서드에는 @IBAction을 제외한 코드로 작성을 한다.

그다음은 viewDidLoad에 버튼과 액션을 연결하면 된다.

Target-Action을 구현할때는 UIControl 클래스가 제공하는 addTarget 메서드를 사용한다.

<img width="453" alt="스크린샷 2021-01-07 오후 8 22 07" src="https://user-images.githubusercontent.com/70311145/103887220-0c2fd300-5126-11eb-8643-a6686eb0d236.png">

1. 첫번째 파라미터는 Target을 전달하는데, 여기서는 Action메서드가 구현되어있는 CodeViewController 인스턴스가 Target이여서 **self**를 전달한다.

2. 두번째 파라미터는 selector을 전달하는데 

```swift
override func viewDidLoa() {
  super.viewDidLoad()
  
  let sel = #selector(action(_:))
  btn.addTarget(self, action: sel, for: .touchUpInside)
}
```

sel 이란 상수를 선언하고 #selector를 입력후 메서드이름을 입력하면

selector로 변환되는데 입력하게 되면 컴파일 오류가 발생한다.

<img width="498" alt="스크린샷 2021-01-07 오후 8 26 00" src="https://user-images.githubusercontent.com/70311145/103887842-16060600-5127-11eb-81ac-a46c48229ca7.png">

selector로 전달한 메서드가 Objective-C에 공개되지 않아서 @objc특성을 추가하라고 나와있다. 

Fix 를 클릭하게되면 selector로 선언했던 두번째 메서드에 @objc가 추가된것을 확인할 수 있다.

<img width="500" alt="스크린샷 2021-01-07 오후 8 33 21" src="https://user-images.githubusercontent.com/70311145/103888168-9fb5d380-5127-11eb-8639-f5a652665754.png">

인터페이스 빌더에서의 작성은 @IBAction을 사용하고 @objc특성이 포함되어있기때문에 따로 작성이 필요없지만

코드에서는 반드시 @ojbc 특성을 직접 추가해줘야 한다. 

이제는 컴파일 오류가 사라지고 버튼과 메서드가 잘 연결된것을 확인할 수 있다.

------



위에서 Target-Action 을 통해 인터페이스 빌더와 코드로 연결하는 방법을 알아보았다.

버튼으로 예를 들었지만 UIControl에 속해있는 클래스들은 

인자값의 내용과 Event만 조금씩 바뀔뿐 Target-Action을 적용하는 방법은 비슷하다.

다음 시간에는 UIControl내에 포함된 클래스들의 각각의 속성들과 다루는 법을 배워보아야겠다.


### 참고 자료
- [UIControl](https://developer.apple.com/documentation/uikit/uicontrol)
- [UIControl.state](https://developer.apple.com/documentation/uikit/uicontrol/1618245-state)
- [Event](https://developer.apple.com/documentation/uikit/uicontrol/event)

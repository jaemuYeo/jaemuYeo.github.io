---
title: "API Design Guidelines"
excerpt: "공식문서 공부하기"

categories:
  - swift
tags:
  - function
last_modified_at: 2021-02-28
---

# [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/#naming)

**API란??**

Application Programming Interface의 줄임말로 프로그램들이 서로 상호작용하는 것을 도와주는 매개체이다.

더 자세하게는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가

제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻한다.

API의 역할은 세가지 정도가 있다.

- 모든 접속을 표준화
- 서버와 DB에 대한 출입구 역할
- 애플리케이션과 기기가 원활하게 통신하도록 도움

Swift API 디자인 가이드라인을 숙지하면 좋은점은 개발자들이 코드를 작성하는 방법을

표준화함으로, 간소화되고 빠른 프로세스 처리를 가능하게 한다.

소프트 웨어를 통합할 때 개발자들 간의 협업을 보다 쉽게 해준다.

---

## Fundamentals (기초)

- 사용 시점에서 명확성이 가장 중요한 목표이다.

  메서드와 프로퍼티와 같은 엔티티는 단 한번만 선언되지만 반복적인 사용이 가능하다.

  API를 디자인하여 이러한 용도를 명확하고 간결하게 사용할 수 있도록 한다.

  디자인을 숙지할 때, 단순히 가이드라인을 읽는 것 만으로는 충분하지 않다.

  항상 여러 사용 사례를 보면서 문맥에서 명확하게 사용되는지 확인해야한다.

- 명료함이 간결함보다 더 중요하다.

  Swift 코드는 간결해 질 수 있지만 가장 작은 문자로 가능한 가장 작은 코드를

  실행하는 것이 목적이 아니다.

  Siwft 코드의 간결성은 강 타입 시스템의 부작용이며, 자연스럽게 상용문을 감소시키는 특징이다.

- 모든 선언에 대해 주석을 작성한다.

  문서화를 통해 얻은 인사이트들은 디자인에 상당한 영향을 끼칠 수 있으니 미루면 안된다.

        API의 기능을 간단한 용어로 선언하는 것에 어려움이 있다면 API를 잘 못 디자인 한 것일 수 있다.

<details>
<summary>MORE DETAIL</summary>
<div markdown = "1">

- Swift에 특화된 Markdown 작성

- 선언된 엔티티에 대한 설명을 요약하는 것으로 시작해라.

  종종 API는 선언과 요약으로 부터 완전히 이해할 수 있다.

  ```swift
  /// 동일한 요소를 포함하는 'self'의 'view'를 반환한다.
  /// 역순으로
  func reversed() -> ReverseCollection
  ```

  - 요약에 집중해야한다. 가장 중요한 부분이다.

    훌륭한 많은 문서의 주석은 훌륭한 주석이 전부다.

  - 가능한 마침표로 끝나는 간단한 한문장의 단편으로 사용한다.

    완전한 문장을 사용하지 마라.

  - 함수 또는 메서드가 수행하는 작업과 반환을 설명해라.

    null 효과와 void 반환은 생략해라.

  ```swift
  /// self의 시작 부분에 newHead를 삽입.
  mutating func prepend(_ newHead: Int)

  /// Element 뒤에 'head'가 포함된 'List'를 반환
  /// of 'self'.
  func prepending(_ head: Element) -> List

  /// 비어 있지 않은 경우 'self'의 첫번째 Element에 제거 또는 반환;
  /// 그렇지 않으면 'nil' 반환.
  mutating func popFirst() -> Element?
  ```

  **NOTE.** popFirst와 같은 케이스는 세미콜론으로 구분하여 여러 문장으로 구성.

  - 서브스크립트에 접근하는 내용 설명 시

  ```swift
  /// Accesses the `index`th element.
  subscript(index: Int) -> Element { get set }
  ```

  - 이니셜라이저의 생성 방식 설명 시

  ```swift
  /// Creates an instance containing `n` repetitions of `x`.
  init(count n: Int, repeatedElement x: Element)
  ```

  - 다른 모든 선언에 대해 선언된 엔티티가 무엇인지 설명

  ```swift
  /// A collection that supports equally efficient insertion/removal
  /// at any position.
  struct List {

  /// The element at the beginning of `self`, or `nil` if self is
  /// empty.
  var first: Element?
  ...
  ```

- 선택 사항으로, 하나 이상의 단락과 글머리 기호 항목을 사용하여 문장을 이어나가야한다.

  단락은 빈 줄로 구분되고 완전한 문장을 사용한다.

  - 적절한 경우에 언제든지 요약을 넘어서 정보를 추가하기 위해
    [인식된 기호 문서화 마크업](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW1) 요소를 사용해라

  - [기호 명령 구문](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW13)으로 인식된 글머리 기호 항목을 알고 사용해라. Xcode와 같은 인기 있는 개발 도구는

  다음과 같은 키워드로 시작하는 글머리 기호들에 특별한 처리를 한다.

  | Attention  | Author        | Authors      | Bug       |
  | ---------- | ------------- | ------------ | --------- |
  | Complexity | Copyright     | Date         | Exeriment |
  | Important  | Invariant     | Note         | Parameter |
  | Parameters | Postcondition | Precondition | Remark    |
  | Requirs    | Returns       | SeeAlso      | Since     |
  | Throws     | ToDo          | Version      | Warning   |

</div>
</details>

---

## Naming

### 명확한 사용 촉진

- 이름이 사용되는 코드(변수,상수,함수,클래스 등등)를 읽는 사용자가 모호하지 않도록

  필요한 모든 단어를 포함한다.

  - 예를 들어, 컬렉션 내에서 주어진 위치에 있는 요소를 삭제하는 메소드를 생각보자.

  ```swift
  extension List {
      public mutating func remove(at position: Index) -> Element
  }
  employees.remove(at: x)
  ```

  메서드 시그니쳐에서 at이라는 단어를 생략한다면, 사용자들은 x를 제거할 요소의 위치를

  나타내는 것이 아니라 메서드가 x와 동일한 요소를 검색하고 제거한다고 이해할 것이다.

  ```swift
  나쁜 예: employees.remove(x) // x 삭제하려고??
  ```

---

- 필요없는 말은 생략한다. 이름에 사용된 바로 그 단어는 사용 사이트에서 중요한 정보를 전달해야 한다.

  의미를 명확히 하거나 의미를 모호하게 하지않기 위해 더 많은 단어가 필요할 수 있지만,

  읽는 사람이 이미 보유하고 있는 정보와 중복되는 단어는 생략해야한다.

  특히 타입 정보를 반복하는 단어는 생략해야한다.

  ```swift
  // 나쁜 예

  public mutating func removeElement(_ member: Element) -> Element?

  allViews.removeElement(cancelButton)
  ```

  이 경우 Element라는 단어는 호출 사이트에서 두드러진 어떤 것도 추가하지 않는다.

  ```swift
  // 좋은 예

  public mutating func remove(_ Element) -> Element?

  allViews.remove(cancelButton) // clearer
  ```

  때때로 모호함을 피하기 위해 타입 정보를 반복해야 한다.

  그러나 일반적으로 파라미터의 타입보다는 파라미터의 역할을 설명하는 단어를 사용하는 것이 좋다.

---

- 타입의 제약 사항이 아닌 역할에 따라서 변수, 파라미터 및 관련 타입의 이름을 지정한다.

  ```swift
  // 잘못된 예
  var string = "Hello"
  protocol ViewController {
      associatedtype ViewType : View
  }
  class ProductionLine {
      func restock(from widgetFactory: WidgetFactory)
  }
  ```

  위와 같은 방식은 타입 이름을 용도 변경해도 명확성과 표현성이 최적화되지 않는다.

  대신에 엔티티에 역할을 나타내는 이름을 선택하도록 노력해야 한다.

  ```swift
  // 좋은 예
  var greeting = "Hello"
  protocol ViewController {
      associatedtype ContentView : View
  }
  class ProductionLine {
      func restock(from supplier: WidgetFactory)
  }
  ```

  만약 연관 타입이 프로토콜 제약사항에 매우 단단하게 묶여있는 경우

  프로토콜의 이름 자체가 그 역할이라면, 연관 타입의 이름에 Type을 붙여서 충돌을 피해라.

  ```swift
  protocol Sequence {
      associatedtype Iterator : IteratorProtocol
  }
  protocol IteratorProtocol { ... }
  ```

---

- 파라미터의 역할을 명확히 하기 위해 약한 타입 정보를 보상한다.

  특히, 파라미터의 타입이 NSObject, Any, AnyObject 또는 Int or String과 같은

  기본 타입인 경우 사용 시점의 타입 정보 및 맥락이 완전히 의도를 전달 못할 수 있다.

  아래 예제는 선언은 명확할 수 있지만 사용 위치는 잘 모른다

  ```swift
  // 잘못된 예
  func add(_ observer: NSObject, for keyPath: String)

  grid.add(self, for: graphics) // 애매하다
  ```

  명확성을 가지게 바꾸려면 각 파라미터에 그 역할을 설명하는 명사를 선행해야한다.

  ```swift
  // 좋은 예
  func addObserver(_ observer: NSObject, forKeyPath path: String)
  grid.addObserver(self, forKeyPath: graphics) // clear
  ```

---

### 유창한 사용을 위한 노력

- 문법적인 영어 구문을 사용하는 사이트를 만드는 메서드 및 함수 이름을 선호한다.

  ```swift
  // 좋은 예
  x.insert(y, at: z)          // “x, insert y at z”
  x.subViews(havingColor: y)  // “x's subviews having color y”
  x.capitalizingNouns()       // “x, capitalizing nouns”
  // 나쁜 예
  x.insert(y, position: z)
  x.subViews(color: y)
  x.nounCapitalize()
  ```

  첫 번째 또는 두 번째 인수 후에 유창성이 저하되는 것은

  이 매개변수들이 호출의 의미의 중심에 있지 않을 때 받아들여질 수 있다.

  ```swift
  AudioUnit.instantiate(
    with: description,
    options: [.inProcess], completionHandler: stopProgressBar)
  ```

- 팩토리 메서드의 이름은 "make"로 시작해라.

  ex) x.makeIterator() , x.makeGame()

- 생성자와 팩토리 메소드 호출의 첫 번째 인자는 기본 이름으로 시작하는

  구문을 형성하지 않아야 한다. ex) x.makeWidget(cogCount: 47)

  예를 들어 아래에 호출에 대해 첫 번째 인수는 기본 이름과 동일한 구문의 일부로 읽히지 않는다.

  ```swift
  // 좋은 예
  let foreground = Color(red: 32, green: 64, blue: 128)
  let newPart = factory.makeWidget(gears: 42, spindles: 14)
  let ref = Link(target: destination)
  ```

  이어서, API 작성자는 첫 번째 인자로 문법적 연속성을 만드려고 했다.

  ```swift
  // 나쁜 예
  let foreground = Color(havingRGBValuesRed: 32, green: 64, andBlue: 128)
  let newPart = factory.makeWidget(havingGearCount: 42, andSpindleCount: 14)
  let ref = Link(to: destination)
  ```

  실제로, 전달인자 레이블에 관한 것과 함께 이 가이드라인은 값을 보존하는

  타입 변환을 수행하는 호출이 아니라면 첫 번째 인자는 레이블을 가질 것임을 의미한다.

  ```swift
  let rgbForeground = RGBColor(cmykForeground)
  ```

- 사이드 이펙트에 따라 함수와 메서드의 이름을 지어라.

  - 사이드 이펙트가 없는 것들은 명사 구문으로 읽혀야 한다. x.distance(to: y), i.successor()
  - 사이드 이펙트가 있는 것들은 명령형 동사 구문으로 읽혀야 합니다. print(x), x.sort(), x.append(y)
  - mutating 메서드와 nonmutating 메서드 쌍의 이름을 일관되게 지어라.

    mutating 메소드는 종종 비슷한 의미론을 갖는 nomutating 메소드를 갖지만,

    nonmutating 메소드는 현재 위치에서 인스턴스를 갱신하기보다는 새로운 값을 반환한다.

          동작이 자연스럽게 동사로 설명될 때, 동사의 명령어를 mutating 방법에 사용하고,
          그것에 상응하는 nonmutating 메서드에는 'ed' 또는 'ing'같은 접미사를 붙여 이름을 지어라.

    | Mutating    | Nonmutating        |
    | ----------- | ------------------ |
    | x.sort()    | z = x.sorted()     |
    | x.append(y) | z = x.appending(y) |

    - 동사의 과거분사형을 사용하여 nonmutating 메서드의 이름을 지어라. (usually appending 'ed')
    - 동사가 직접적인 객체라서 'ed'를 붙이는 것이 문법적으로 맞지 않을 때,

      'ing'를 붙여 동사의 현재분사형을 사용하여 nonmutating 메서드의 이름을 지어라.

  - 동작이 순수하게 명사로 묘사될 때, nonmutating 메서드의 이름에 명사를 사용하고

    이에 상응하는 mutating메서드에는 접두사로 form 을 붙여 이름 지어라.

    | Nonmutating        | Mutating            |
    | ------------------ | ------------------- |
    | x = y.union(z)     | y.formUnion(z)      |
    | j = c.successor(i) | c.formSuccessor(&i) |

  - 용도가 nonmutating일 때 불리언 메서드와 함수의 사용은

    assertions about the receiver로 읽혀야 한다. x.isEmpty, line1.intersects(line2)

  - 기능을 설명하는 프로토콜은 접미사 able, ible 또는 ing를 붙여 이름을 사용한다.

    (e.g. Equatable, ProgressReporting).

  - 다른 타입, 프로퍼티, 변수 그리고 상수의 이름은 명사로 읽혀져야 한다.

---

### 용어를 잘 사용하기

> Term of Art - 명사. 특정 분야나 직업 내에서 정확하고 전문화된 의미를 갖는 단어 또는 구절이다.

- 더 일반적인 단어가 의미를 전달하는 경우에 **모호한 용어는 피해야한다.**

  'skin'이 당신의 목적에 맞다면 'pepidermis'는 피해라.

  전문 용어는 필수적인 의사소통 도구이지만, 그것이 아니라면 잃어버릴 중요한

  의미를 포착하는 데만 사용해야 한다.

- 전문 용어를 사용한다면 확립된 의미를 고수해라.

  - 보다 일번적인 단어가 아닌 기술 용어를 사용하는 유일한 이유는

    모호하거나 불분명한 것을 정확하게 표현하기 때문이다.

    따라서 API는 수용된 의미에 따라 용어를 엄격하게 사용해야 한다.

          <전문가를 놀라게 하지마라>
          이미 그 용어에 익숙한 사람이라면 누구나 놀라고 아마 우리가 이용어에 대한
          새로운 의미를 발명한 것처럼 보인다면 화가 날 것이다.
          <초보자를 혼동하지 마라>
          그 용어를 배우려는 사람은 누구나 웹 검색을 하고 그에 대한 전통적인
          의미를 찾을 가능성이 있다.

- 약어의 사용을 피해라.

  특히 비표준 축약형은 효과적인 전문용어가 된다.

  그것을 이해하는 것은 축약형이 아닌 형태로 올바르게 변환하는 데 달려있기 때문이다.

  > 어떠한 축약형이 의도하는 의미는 웹 검색을 통해 쉽게 찾을 수 있어야 한다.

- 선례를 받아들여라.

  - 기존 문화에 순응하는 데 희생하면서 전체 초보자에 대한 용어를 최적화하지 마라.

    초보자가 List의 의미를 더 쉽게 파악할 수 있음에도 불구하고

    List와 같은 단순화된 용어를 사용하는 것보다 연속적인 데이터 구조 배열의 이름을

    지정하는 것이 더 낫다. Array는 현대 컴퓨팅에서 기본이므로 모든 프로그래머는

    Array가 무엇인지 알고 있거나 곧 알게 될 것이다. 대부분의 프로그래마가

    익숙한 용어를 사용하면 웹 검색과 질문에서 답을 얻기 쉬울 것이다.

  - 수학과 같은 특정한 프로그래밍 도메인에서, sin(x) 와 같은 널리 선행된 용어는

    verticalPositionOnUnitCircleAtOriginOfEndOfRadiusWithAngle(x)

    같은 설명 구절보다 선호됩니다.

    이 경우에, sine 이라는 완전한 단어가 있을지라도 sin(x)는

    수십 년간 프로그래머들 사이에서, 몇 세기동안 수학자들 사이에서 흔하게 사용되었으므로,

    선례는 축약형을 피하라는 가이드라인의 중요도보다 높습니다.

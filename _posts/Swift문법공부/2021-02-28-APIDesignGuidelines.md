---
title: "API Design Guidelines"
excerpt: "공식문서 공부하기"

categories:
  - swift
tags:
  - function
last_modified_at: 2021-02-28
---

# API Design Guidelines 읽어보기

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
</div>
</details>

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

      <details>
      <summary>MORE DETAIL</summary>
      <div markdown = "1">
      - 적절한 경우에 언제든지 요약을 넘어서 정보를 추가하기 위해 
           [인식된 기호 문서화 마크업](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW1) 요소를 사용해라
      </div>
      </details>

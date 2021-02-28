---
title: "Siwft) Collection Types"
excerpt: "공식문서 공부하기"

categories:
  - swift
tags:
  - CollectionTypes
last_modified_at: 2021-02-28
---

# [Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html)

스위프트는 값을 저장하기 위한 array,set 그리고 Dictionary 세가지 컬렉션 타입을 제공한다.

Array는 값의 집합을 정렬한다. Set은 고유 값의 순서가 없는 집합이다.

Dictionary는 키-값으로 연결된 정렬되지 않은 컬렉션이다.

 <img width="657" alt="스크린샷 2021-02-28 오후 10 41 02" src="https://user-images.githubusercontent.com/70311145/109420482-154a6b80-7a16-11eb-8c79-a49115612d5f.png">

Array, Set, Dictionary는 저장 시 키와 값의 타입이 명확해야 한다.

이것은 잘못된 타입의 값을 실수로 컬렉션에 저장할 수 없다는 것을 의미한다.

또한 컬렉션에서 검색할 값의 타입에 대해 자신 있게 생각 할 수 있다.

> Note. 스위프트의 Array, Set, Dictionary 타입은 [제네릭](https://docs.swift.org/swift-book/LanguageGuide/Generics.html) 컬렉션으로 구현된다.

## 가변 컬렉션(Mutability of Collections)

Array, Set, Dictionary를 변수에 할당하면 작성된 컬렉션이 변경될 수 있다.

이는 컬렉션에 항목을 추가, 제거 또는 변경하여 컬렉션을 만든 후 컬렉션을 변경 할 수 있다는 것을 말한다.

반면 상수에 할당하면 해당 컬렉션은 불변이며 크기와 내용은 변경할 수 없다.

        컬렉션이 변경될 필요가 없는 모든 경우에 불변의 컬렉션을 만드는 것이 좋은 습관이다.
        그 이유는 코드에 대해 쉽게 추론할 수 있고, 스위프트 컴파일러가 작성한
        컬렉션의 성능을 최적화할 수 있다.

## 배열(Arrays)

배열 같은 타입들을 정렬된 순서로 저장한다. 동일한 값이 배열의 여러 위치에서 여러번 나타날 수 있다.

- Swift의 Array 타입은 [NSArray class](https://developer.apple.com/documentation/swift/array#2846730)와 연관되어있다.

---

### 축약 배열 타입 문법(Array Type Shorthand Syntax)

스위프트 Array의 타입은 Array<Element>로 작성된다. 여기서 Element는

배열이 저장할 수 있는 값의 타입이다. 간단한 방법으로 [Element]로 배열의 타입을 쓸 수 있다.

Array<Element>와 [Element]는 기능적으로 동일하지만, 간단한 방법을 선호한다.

---

### 빈 배열 생성(Creating an Empty Array)

초기화를 통해 특정 타입의 빈 배열을 만들 수 있다.

```swift
var someInts = [Int]()
print("someInts is of type [Int] with \(someInts.count) items.")
// "someInts is of type [Int] with 0 items."
```

someInts 변수의 타입은 초기화 타입으로부터 [Int]로 추론된다는 점에 유의.

[]를 사용하여 이미 함수의 인수 또는 값이 저장된 변수, 상수와 같은 타입의 정보를

제공하는 경우 빈 배열을 만들 수 있다.

```swift
someInts.append(3) // 배열에 값 1개 추가
someInts = [] // 빈 배열이 되었지만 여전히 타입은 Int

```

---

### 기본 값을 사용한 배열 생성

Array 타입은 모든 값이 동일한 기본값으로 설정된 특정 크기의 배여을 만드는 초기화를 제공한다.

초기화에 적절한 타입(repeating:)의 기본값을 전달하고,

그 값이 새 배열(count:)에서 반복되는 횟수를 정한다.

```swift
var threeDoubles = Array(repeating: 0.0, count: 3)
// 타입은 [Double]가 되고, 같은 표현으로 [0.0, 0.0, 0.0]
```

---

### 두개의 배열을 함께 추가하여 배열 작성(Creating an Array by Adding Two Arrays Together)

더하기 연산자(+)를 사용하여 같은 타입의 배열을 합쳐서 새 배열을 만들 수 있다.

새 배열의 타입은 연산했던 두 배열의 타입을 추론하여 나타난다.

```swift
var threeDoubles = Array(repeating: 0.0, count: 3)
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// [Double]타입, 같은 표현으로 [2.5, 2.5, 2.5]

var sixDoubles = threeDoubles + anotherThreeDoubles
// 추론된 타입은 [Double], 같은 표현으로 [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

---

### 배열 리터럴을 통한 배열 생성(Creating an Array with an Array Literal)

배열 리터럴을 사용하여 배열을 초기화 할 수 있다. 이 리터럴은 배열 컬렉션으로

하나 이상의 값을 단축하는 방법이다. []에서 쉼표를 통해 값의 목록을 작성한다.

> [value1, value2, value3]

```swift
var shoppingList: [String] = ["Beer", "Milk", "Egg"]
// 문자열 타입의 배열에 세개의 값이 초기값으로 지정
```

변수로 선언시 리터럴 값을 추가 또는 삭제할 수 있다. 상수는 불가능.

스위프트의 타입 추론 덕분에 [Stiring]은 사용하지 않아도 된다.

```swift
var shoppingList = ["Beer", "Milk", "Egg"]
```

리터럴 내부에 모든 값이 동일한 타입이기 때문에 [String]이 위 변수에 사용하기 올바른 타입이라고 추론할 수 있다.

### 배열 접근 및 수정

배열의 메서드와 프로퍼티를 통해 서브스크립트하여 접근하고 수정한다.

읽기 전용인 count 속성을 통해 배열의 인덱스 수를 확인할 수 있다.

```swift
var numberArray = [1, 2, 3]

print("numberArray 변수에 들어있는 값의 수는 \(number.count)이다.")
// "numberArray 변수에 들어있는 값의 수는 3이다."
```

if 문과 isEmpty 속성을 통해 배열의 값이 비었는지 확인할 수 있다.

```swift
if numberArray.isEmpty {
    print("numberArray에 값은 비어있다. ")
} else {
    print("numberArray에 값이 있다.")
}
// "numberArray에 값이 있다."
```

append(\_:)메서드를 통해 배열의 끝에 값을 추가할 수 있다.

```swift
numberArray.append(4)
```

+= 추가 할당 연산자를 통해 같은 타입의 호환에 따라 항목을 추가한다.

```swift
numberArray += [5]
numberArray += [6,7,8]
```

서브스크립트 문법을 통해 배열에서 값을 검색할 수 있다.

검색할 배열의 이름 뒤에 []를 붙이고 검색할 인덱스를 전달한다.

```swift
var firstNumber = numberArray[0] // 1
```

> 배열의 인덱스의 첫 번째는 항상 0에서 부터 카운트 한다.

서브스크립트 문법을 사용하여 지정된 인덱스의 기존 값을 변경할 수 있다.

```swift
numberArray[0] = 2021
// 0번째 인덱스 값인 1이 2021로 변경된다.
```

배열의 길이가 변경하려는 범위와 다른 경우에도 서브스크립트 문법을 사용하여

값 범위를 한번에 변경할 수 있다.

```swift
numberArray[4...6] = [100, 200]
// 4,5,6인덱스 배열 세개를 100,200 두개의 값만 인덱스로 변경
```

insert(\_:at:)메서드를 활용하여 지정한 인덱스 배열에 항복을 삽입할 수 있다.

```swift
numberArray.insert(28, at: 0)

numberArray[0] // 28
```

삽입할 수 있다면 반대로 remove(at:)메서드를 활용하여 입력 된 인덱스의 값을 제거할 수 있다.

이 메서드는 항목이 제거된 후 항목을 반환하지만 필요에 따라 반환 값을 무시할 수 있다.

```swift
let number = numberArray.remove(at: 0)
// numberArray의 0번째 인덱스인 28이 제거
// 이제 numberArray배열에는 28 값이 없음
// 상수 number에 28일 반환
```

        배열의 기존 한계를 벗어난 인덱스의 값에 접근하거나 수정하려고 하면
        런타임 오류가 발생한다. 인덱스를 사용하기 전에 해당 인덱스를 배열의 개수 속성가
        비교하여 유효한지 확인할 수 있다. 배열이 0에서 인덱싱되므로 배열에서
        가장 큰 유효한 인덱스는 카운트 -1 이지만, 카운트가 0(빈 배열)이면 유효한 인덱스가 없다.

removeLast() 메서드를 활용하면 배열의 마지막 인덱스를 제거할 수있다.

remove(at:)메서드와 마찬가지로 제거된 항목을 반환한다.

```swift
let lastNumber = numberArray.removeLast()
```

---

### 배열 반복하기(Iterating Over an Array)

for-in 루프가 있는 배열의 전체 값 집합에 대해 반복할 수 있다.

```swift
var shoppingList = ["eggs", "Milk", "Flour", "Bananas", "Apple"]

for item in shoppingList {
    print(item)
}
// Six eggs
// Milk
// Flour
// Bananas
// Apple
```

각 항목의 정수 인덱스와 해당 값이 필요한 경우 enumerated()메서드를 활용하여

배열을 대신 반복할 수 있다. 배열의 각 항목에 대해 enumerated()메서드는 정수와 항목으로

구성된 튜플을 반환한다. 정수는 0에서 시작하여 각 항목에 대해 하나씩 카운트 된다.

전체 배열에 걸쳐 열거하면 이 정수가 항목의 인덱스와 일치한다.

반복의 일부로 튜플을 임시 상수 또는 변수로 분할 가능 하다.

```swift
for (index, value) in shoppingList.enumerated() {
    print("Item \(index + 1): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Banana
// Item 5: Apple
```

---

## Set

Set은 정렬되지 않은 배열에 동일한 타입의 고유한 값을 저장한다.

항목 순서가 중요하지 않거나 항목이 한번만 나타나도록 할 때 Array 대신 Set을 사용할 수 있다.

> Swift의 Set 타입은 Foundation의 [NSSet 클래스](https://developer.apple.com/documentation/swift/set#2845530)와 브리지 된다.

---

### Set 타입에 대한 해시 값(Hash Values for Set Types)

Set에 저장하려면 타입이 해시 가능해야 한다.

즉, 타입이 해시 값을 계산하는 방법을 제공해야 한다.

해시 값은 동등하게 비교하는 모든 개체에 대해 동일한 Int 값으로서,

a == b 인 경우 a의 해시 값이 b의 해시 값과 같다.

스위프트의 모든 타입은 기본적으로 해시 가능하며, 설정 값 타입이나

Dictionary 키 타입으로 사용할 수 있다.

연관된 값이 없는 열거형 associated 값도 기본적으로 해시할 수 있다.

        스위프트의 표준 라이브러리의 hashable 프로토콜을 준수하도록 하여 커스텀 타입을
        값 타입 또는 Dictionary 값 타입으로 사용할 수 있다.


---

### Set 타입 설정

스위프트의 Set 타입은 Set<Element>로 쓰이며, Element는 Set이 저장할 수 있는 타입이다.

Array와 달리 Set에는 동일한 속기 형식이 없다.

---

### 비어있는 Set 생성 및 초기화(Creating and Initializing an Empty Set)

이니설라이저를 사용하여 특정 타입의 빈 Set을 생성할 수 있다.

```swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// "letters is of type Set<Character> with 0 items."
```

        letters 변수의 타입은 이니셜라이저의 타입에서 Set<Character>로 유추된다.

컨텍스트가 이미 함수 인수 또는 이미 입력된 변수, 상수와 같은 타입 정보를

제공하는 경우 빈 배열 리터럴이 있는 빈 Set을 만들 수 있다.

```swift
letters.insert("a")
// 문자에는 이제 문자 타입의 값이 1개 포함되어있다.
letters = []
// 빈 집합이 되었지만 여전히 타입은 Set<Character>이다.
```

---

### 배열 리터럴을 사용하여 Set 생성(Creating a Set with an Array Literal)

하나 이상의 값을 Set 컬렉션으로 쓰는 짧은 방법으로는 배열 리터럴로 Set을 초기화 하는 것이다.

```swift
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
// 세개의 항목으로 초기화
```

favoriteGenres 변수에 문자열 값 집합으로 선언 되고 Set<String>으로 작성한다.

문자열의 값 타입만 선언했으므로 문자열 값만 저장할 수 있다. 현재는 세 가지 문자열 값으로 초기화 했다.

        값이 추가되거나 제거 될 수 있으므로 변수로 선언

집합 타입은 배열 리터럴에서만 유추할 수 없으므로 집합 타입을 명시적으로 선언해야 한다.

그러나 스위프트의 타입추론으로 인해 한 타입의 값만 포함하는 배열 리터럴로 초기화하는 경우에는

집합의 타입 요소를 쓸 필요가 없다.

```siwft
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
```

배열 리터럴의 모든 값이 동일한 타입이기 때문에 스위프트는

Set<String>이 변수에 사용할 올바른 타입이라고 추론할 수 있다.

---

### Set 접근 및 수정(Accessing and Modifying a Set)

메스드 및 프로퍼티를 통해 집합에 접근하고 수정할 수 있다.

count 속성을 통해 집합의 항목 수를 읽기 전용으로 확인할 수 있다.

```swift
print("I have \(favoriteGenres.count) favorite music genres.")
// Prints "I have 3 favorite music genres."
```

isEmpty 속성을 통해 count속성이 0과 동일한지 여부를 확인할 수 있다.

```swift
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
// Prints "I have particular music preferences."
```

insert(\_:)메서드를 호출하여 집합에 새 항목을 추가할 수 있다.

```swift
favoriteGenres.insert("Jazz")
// favoriteGenres now contains 4 items
```

remove(\_:)메서드를 호풀하여 집합의 맴버인 경우 항목을 제거할 수 있고,

집합에 항목이 포함되어 있지 않으면 0을 반환한다.

또는 removeAll()메서드를 호출하여 집합의 모든 항목을 제거할 수 있다.

```swift
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}
// Prints "Rock? I'm over it."
```

contains(\_:)메서드를 호출하여 집합에 특정 항목이 포함되어 있는지 확인할 수 있다.

```swift
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// Prints "It's too funky in here."
```

---

### Set에서 반복(Iterating Over a Set)

for-in 반복문을 사용하여 집합의 값을 반복할 수 있다.

```swift
for genre in favoriteGenres {
    print("\(genre)")
}
// Classical
// Jazz
// Hip hop
```

스위프트에서 Set 타입은 정렬되어 있지 않다.

특정 순서로 집합의 값을 반복하려면 sorted()메서드를 사용한다.

sorted() 메서드는 > 연산자를 사용하여 정렬된 배열로 반환한다.

```swift
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
```

---

## Set 동작 수행(Performing Set Operations)

집합의 동작 수행에는 네가지가 있다.

- 두 집합을 결합
- 두 집합에서 공통되는 값을 확인
- 두 집합이 동일한 값을 모두 포함하는지
- 일부 또는 전혀 포함하지 않는지 확인

### 기본 집합 작업(Fundamental Set Operations)

![스크린샷 2021-03-01 오전 1 43 09](https://user-images.githubusercontent.com/70311145/109426161-7d597b80-7a2f-11eb-974f-e8bc47835824.png)

- intersection(\_:) - 두 집합 모두에 공통적인 값만 사용하여 새 집합을 생성
- symmertricDifference(\_:) - 두 집합 모두 값은 아니지만 두 집합 모두로 새 집합을 생성
- union(\_:) - 두 집합의 모든 값으로 새 집합을 생성
- subtracting(\_:) - 지정된 집합에 없는 값을 사용하여 새 집합을 생성

```swift
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]

oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]
```

---

### 구성원 자격 설정과 평등(Set Membership and Equality)

그림은 집합 간에 공유되는 요소를 나타내는 영역이 겹치는 세 집합을 보여준다.

a는 b의 모든 요소를 포함하므로 집합 a는 집합 b의 상위 집합이 된다.

반대로 b의 모든 요소도 a에 의해 포함되기 때문에 집합 b는 a의 하위 집합이다.

집합 b와 집합 c는 공통적인 요소가 없기때문에 벤드 세트 케어가 서로 분리되어 있다.

![스크린샷 2021-03-01 오전 1 53 11](https://user-images.githubusercontent.com/70311145/109426393-e68dbe80-7a30-11eb-8001-1af6a9ed0777.png)

- = 'is equal' 연산자 - 사용하여 두 집합에 동일한 값이 모두 포함되어 있는지 확인
- isSubset(of:) - 집합의 모든 값이 지정된 집합에 포함되어 있는지 여부를 결정
- isSuperset(of:) - 집합에 지정된 집합의 모든 값이 포함되어 있는지 여부를 결정
- isStricSubset(of:) or isStrictSuperset(of:)

  집합이 지정된 집합인지 또는 수퍼셋인지 여부를 결정

- isDisjoint(with:) - 두 집합에 공통 값이 없는지 여부를 결정

```swift
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
```

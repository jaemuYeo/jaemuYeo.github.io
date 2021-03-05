---
title: "Siwft) Struct and Class"
excerpt: "공식문서 공부하기"

categories:
  - swift
tags:
  - StructClass
last_modified_at: 2021-03-05
---

# Struct and Class

구조체와 클레스는 프로그램 코드 블럭을 만들도록 유연하게 구성하는 것이 목적이다.

프로퍼티와 메서드는 구조체와 클래스에 상수,변수,함수로서 동일한 구문을 정확하게

사용하여 기능을 추가하도록 정의한다.

**클래스 인스턴스는 전통적으로 객체로 알려져 있다.**

그러나 스위프트 클래스와 구조체는 다른 언어보다도 **기능**에 더 가깝다.

아래 코드는 Person(사람)을 비교하여 코드를 연습했다.

사람이라는 클래스 인스턴스를 만들어서 이름,나이,키,몸무게와 같은 속성(프로퍼티)를

얻을 수 있고, 동작(메서드)을 구현하게 되면 그 사람이 하는

행동을 비유할 수 있다(예. 홍길동이 달린다, 홍길동이 밥먹는다 등등..)

---

### 구조체와 클래스 비교

- 비슷한 점

  - 값을 저장하는 속성을 정의(프로퍼티)
  - 기능을 제공하는 메서드를 정의(메서드)
  - 서브스크립트 구믄을 사용하요 값을 접근할 수 있는 서브스크립트를 정의
  - 초기 상태를 설정하는 초기화 정의 (이니셜라이저)
  - 기본적인 구현을 넘어선 기능을 확장시킬 수 있도록 확장이 가능(익스텐션)
  - 특정 종류의 표준 기능을 제공하는 프로토콜을 따름(프로토콜)
  - 이름 정의 시 UpperCamelCase사용 ( SomeClass. SomeStruct )

- 차이점
  - 구조체는 상속 X
  - 타입캐스팅은 클래스의 인스턴스만 허용 ( is as )
  - 디이니셜라이저는 클래스의 인스턴스에서만 활용
  - 클래스는 참조 타입, 구조체는 값타입 (구조체를 전달할 때는 항상 값이 복사됨)

### Class(클래스)와 struct(구조체)

```swift
// 클래스 선언
class SomeClass {

}

// 구조체 선언
struct SomeStruct {

}

// 클래스와 구조체 인스턴스 생성
var someClass = SomeClass()
var someStruct = SomeStruct()

// 클래스와 구조체 속성 접근
// 도트 (.)을 사용하여 속성에 접근.
struct Body {
    var height = 185
    var weight = 70
}

class Person {
    var bady = Body()
    var name: String = ""
    var age: Int = 15
}
var person = Person()
print("Henry의 나이는 \(person.age)살 입니다.")
// Henry의 나이는 15살 입니다.

// 클래스안에 선언된 구조체 인스턴스를 통해 값에 접근 가능.
print("Henry의 키는 \(person.bady.height)cm 입니다.")
// Henry의 키는 185cm 입니다.

// 클래스는 초기화 값을 가지거나 이니셜라이저 해야하지만 구조체는 기본값 없이 타입만 선언가능

class Person {
    var name: Stirng = ""
    var age: Int = 0
}
// 또는
class Person {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}
// 옵셔늘을 이용하여 값을 안줘도 됨.
class Person {
    var name: String?
    var age: Int?
}

// 구조체는 옵셔늘을 하지 않아도 값 없이 선언가능
struct Person {
    var name: Sting
    var age: Int
}
```

모든 구조체는 자동 생성된 멤버 초기화를 가지며,

이는 새로운 구조체 인스턴스의 멤버 속성을 초기화 하도록 사용할 수 있다.

새로운 인스턴스의 속성을 위한 초기 값은 이름을 멤버 초기화에다 넘겨준다.

```swift
struct Person {
    var name: String = ""
    var age : Int = 0
}
var person = Person(name: "Henry", age: 15)
```

### 구조체는 값 타입

값 타입은 타입이며 이 값은 상수나 변수에 할당하거나 함수에 넘겨질 때 복사된다.

스위프트에서 기본 타입은 모두 값 타입. Int, Double, Array, Dictionay, String 등등..

생성하는 모든 구조체와 열거형 인스턴스(모든 값 타입은 속성으로 가짐)는 코드 내에 전달될 때 항상 복사된다.

```swift
struct Person {
    var name: String
    var age: Int
}
let member1 = Person(name: "Henry", age: 20)
var member2 = member1
member2.name = "Jamking"

print("member1의 이름은 \(member1.name)이다.")
// member1의 이름은 Henry이다.
print("member2의 이름은 \(member2.name)이다.")
// member2의 이름은 Jamking이다.
```

### 클래스는 참조 타입

값 타입과는 다르게 참조 타입은 변수나 상수에 할당하거나 함수에 넘길 때 복사하지 않는다.

복사 대신에 기존에 같은 인스턴스에 참조가 사용된다.

```swift
class Person {
    var name: String?
    var age: Int?

}

let member1 =  Person()
member1.name = "Henry"
member1.age = 15

let member2 = member1
member2.name = "Jamking"

print("member1의 name은 \(member1.name)")
// member1의 name은 Jamking
```

member1과 member2는 같은 Person 인스턴스를 참조한다.

사실상 동일한 하나의 인스턴스를 두개의 다른 이름으로 가진다.

member1과 member2는 Person인스턴스를 저장하는 것이 아니고 참조만 한다.

잠재적인 Person에 name은 변경되지만 Person에 상수 참조 값은 변경되지 않는다.

### 언제 클래스를 쓰고 언제 구조체를 쓰는지??

프로그램 코드의 구성된 블럭으로서 사용자 데이터 타입으로 정의하는 클래스나 구조체를 사용할 수 있다.

그러나 구조체 인스턴스는 값을 항상 넘기며, 클래스 인스턴스는 항상 참조를 넘겨준다.

프로젝트에 필요한 데이터 구조와 기능을 고려하여, 각각의 데이터는 클래스나 구조체로 정의하도록 구성해야한다.

구조체를 생성 시 아래의 조건에 한 가지 이상일 경우 적용

- 구조체의 최우선 목표는 몇몇 단순 데이터 값을 캡슐화 할 때
- 캡슐화된 값이 그 구조체의 인스턴스가 할당되거나 넘겨질 때 참조보다 복사하는 것일 때
- 구조체에 저장되는 값 속성이 참조보다 복사가 예상되는 값 타입일 때
- 다른 기존 타입에서 기능이나 속성이 상속될 필요가 없을 때

당연 클래스는 위 조건의 반대일 때??

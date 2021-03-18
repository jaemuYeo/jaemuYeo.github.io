---
title: "Singleton Pattern"

categories:
  - swift

tags:
  - [singleton]

toc: true

toc_sticky: true

date: 2021-03-17

last_modified_at: 2021-03-17
---

# [Singleton Pattern](https://developer.apple.com/documentation/swift/cocoa_design_patterns/managing_a_shared_resource_using_a_singleton)

싱글톤 패턴은 객체를 하나만 생성하여, 생성된 객체를 어디서든 참조할 수 있도록 하는 패턴이다.

## Overview

싱글 톤을 사용하여 전역 적으로 액세스 가능한 클래스의 shared 인스턴스를 제공한다.

사운드 효과를 재생하는 오디오 채널 또는 HTTP 요청을 수행하는 네트워크 관리자와 같이

앱에서 공유되는 리소스 또는 서비스에 대한 통합 액세스 포인트를 제공하는 방법으로

고유한 싱글톤을 만들 수 있다.

---

## 싱글톤 생성 방법

여러 스레드에서 동시에 액세스하더라도 한 번만 지연 초기화되도록 보장되는

static 타입 프로퍼티를 사용하여 간단한 싱글톤을 만든다.

```swift
class Singleton {
    static let sharedInstance = Singleton()
}
```

초기화 이외의 추가 설정을 수행해야하는 경우 클로저 호출 결과를 전역 상수에 할당 할 수 있다.

```swift
class Singleton {
    static let sharedInstance: Singleton = {
        let instance = Singleton()
        // 설정 코드
        return instance
    }()
}
```

---

## 조금 더 자세히 알아보기

```swift
// 아래 클래스는 클라이언트가 고유 한 싱글 톤 인스턴스에 액세스 할 수있는 '공유'필드를 정의한다.

class Singleton {
    // 싱글톤 인스턴스에 대한 액세스를 제어하는 정적 필드이다.
    // 각 하위 클래스의 인스턴스를 하나만 유지하면서 Singleton 클래스를 확장 할 수 있다.
    static var shared: Singleton = {
        let instance = Singleton()
        // 이 곳에 인스턴스 구성
        return instance
    }()
    // 싱글톤 이니셜라이저는 항상 비공개여야한다.
    // 혹시라도 init함수를 호출해 인스턴스를 또 생성하는 것을 막기위해.
    private init()
    // 마지막으로 모든 싱글 톤은 인스턴스에서 실행할 수있는 비즈니스 로직을 정의해야한다.
    func someBusinessLogic() -> String {
        // 함수 내용
        return "호출 결과"
    }
}

// 싱글톤은 복제할 수 없어야 한다.
extension Singleton: NSCopying {

    func copy(with zone: NSZone? = nil) -> Any {
        return self
    }
}

// 클라이언트 코드 (예를들어 VC)
class Client {
    static func someClientCode() {
        let instance1 = Singleton.shared
        let instance2 = Singleton.shared

        if (instance1 == instance2) {
            print("싱글톤이 호출되며 두 변수 모두 동일한 인스턴스를 포함한다.")
        } else {
            print("싱글톤 실패, 변수에 다른 인스턴스가 포함되어있다.")
        }
    }
    // ...
}
```

[NSCopying 프로토콜](https://developer.apple.com/documentation/foundation/nscopying)

---

## 정리

**싱글톤 장점**

- 한 번의 인스턴스만 생성하므로 메모리 낭비를 방지한다.
- 싱글톤의 인스턴스는 전역인스턴스라서 다른 클래스들과 자원 공유가 쉽다.
- 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 쓰인다.

**싱글톤 단점**

- 싱글톤 인스턴스가 너무 많은 일을 하거나, 많은 데이터를 공유시킬 경우
  다른 클래스의 인스턴스들 간 결합도가 높아져 '개방=폐쇄'원칙에 어긋남. (oop 설계 원칙)
  그러므로 수정과 테스트가 어려워진다.

**iOS에서의 싱글톤 사용예**

```swift
let screen = UIScreen.main
let userDefault = UserDefaults.standard
let application = UIApplication.shared
let fileManager = FileManager.default
let notification = NotificationCenter.default
```

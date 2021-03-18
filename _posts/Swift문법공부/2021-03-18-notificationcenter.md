---
title: "NotificationCenter"

categories:
  - swift

tags:
  - [NotificationCenter]

toc: true

toc_sticky: true

date: 2021-03-18

last_modified_at: 2021-03-18
---

# [NotificationCenter](https://developer.apple.com/documentation/foundation/notificationcenter)

등록 된 관촬자(Observer)에게 정보를 브로드 캐스트 할 수 있는 Notification dispatch 메커니즘이다.

NotificationCenter에 등록된 이벤트가 발생하면 해당 이벤트들으ㅔ 대한 행동을 취한다.

앱 내에서 아무곳에서 메세지를 던지면 앱 내의 아무곳에서 이 메세지를 받을 수 있게 해주는 역할을한다.

## 노티피케이션 센터가 필요한 이유는 무엇일까??

모바일앱 개발에서는 때때로 핸들러 방향과 같은 요구 사항을 구현하고,

한 클래스에서 다른 클래스로 데이터를 전달하고, 다른 메서드나 함수를 호출 할 것이다.

두 클래스의 의사 소통에 가장 좋은 방법인 **Delegate 패턴**이 있지만 Delegation은

싱글 브로드캐스팅이나 메서드를 동시에 알리는 데 도움이 되지 않는다.

**NotificationCenter의 몇 가지 장점**

- 한 클래스에서 여러 클래스로 싱글을 관찰하고 브로드캐스팅하는 데 도움이 된다.

- 한 클래스에서 여러 클래스로 싱글을 포스트한다. (다수 객체들에게 동시에 이벤트 발생을 알림)

- 여러 클래스에서 신호를 수신한다.

## 관찰을 위한 NotificationCenter 등록

```swift
NotificationCenter.default.addObserver(self, selector: #selector(loginSuccess), ("com.user.login.success"), object: nil)
```

이 코드는 수신을 위한 Notification 등록 절차이다. `NotificationCenter`를 기반으로 관찰 할 수 있다.

- NotificationCenter.default - 더 많은 알림이 있는 경우 클래스 네에서 전역적으로
  만들 수 있는 알림 변수이다.

- addObserver(self, - Observer Notification을 받을 클래스를 위한 것이다.

- selector: #selector(loginSuccess) - Notification이 이 메서드 호출을 수신 할 때의 메서드 이름이다.

- name: NSNotification.Name(“com.user.login.success”) - Notification 키이며 새 알림 등록 방법에
  대해 고유해야한다. 동일한 메서드를 호출하려면 동일해야한다. 키는 Key 및 lock로 등록한
  동일한 메서드만 호출 할 수 있다.

- object: nil) - 객체 내에서 모든 객체 또는 변수 값(Bool, String, Dictionary, Array, Int ,,,)을
  전달할 수 있다. 현재는 이 프로세스에서 값을 전달하지 않기 때문에 nil 값이 설정되어 있다.

## NotificationCenter에 데이터를 Post하는 방법.

Notification의 도움을 받아 위의 메서드를 호출한다. 이 부분은 마치 Broadcaster(방송인)과 같다.

동일한 클래스가 필요하지 않은 곳에서 Notification 메서드를 호출한다.

옵저버의 Key를 기반으로 식별한다. 이 post Notification으로 데이터를 전달 할 수도 있다.

```swift
NotificationCenter.default.post(name: NSNotification.Name("com.user.login.success"), object: nil)
```

## Notification 메서드로 데이터를 전달하고 받는 방법.

Step1 - 먼저 @objc로 메서드 이름을 작성한다.

왜?? 때로 Objective-C 코드는 Swift 코드와 상호작용하며 Objective-C 코드에서

활성화되어야하므로 @objc가 필요한 이유이다.

```swift
@objc func loginSuccess(_ notification: Notification) {
    // 코드 내용
}
```

Step2 - 수신자(NotificationCenter Observer 등록)

```swift
NotificationCenter.default.addObserver(self, selector: #selector(loginSuccess(_:)), ("com.user.login.success"), object: nil)
```

Step3 - Post Notification

```swift
let loginResponse = ["userInfo": ["userID": 4, "userName": Henry]]

NotificationCenter.default.post(name: NSNotification.Name("com.user.login.success"), object: nil, userInfo: loginResponse)
```

Step4 - 유저 데어터 수신 핸들

```swift
@objc func loginSuccess(_ notification: Notification) {
    print(notification.userInfo?["userInfo"] as? [String: Any] ?? [:])
}
// ["userID": 4, "userName": "Henry"]
```

Step5 - Notification 제거

```swift
deinit {
    NotificationCenter.default.removeObserver(self, name: NSNotification.Name("com.user.login.success"), object: nil)
}
```

마지막으로 프로젝트 내에서 Key를 다시 작성하는 실수를 피하기 위해 Extension내에서

Notification Key를 정의하면 된다. 현업 프로젝트에서 수동으로 변경할 수 있는 방법이라고 한다.

```swift
extension Notification.Name {
    static var loginSusccess: Notification.Name {
        return .init(rawValue: "UseLogin.success")
    }
    static var verifyUserSession: Notification.Name {
        return .init(rawValue: "VerifyUser.session")
    }
}
```

### Use Case

위에 정의한 코드를 통해 `NSNotification.Name("com.user.login.success")`대신

간한하게 `.loginSuccess`를 작성할 수 있다.

```swift
NofiticationCenter.default.addObserver(self, selector: #selector(loginSuccess(_:)), name: .loginSuccess, object: nil)
```

## class 내에서 NotificationCenter 활용해보기

```swift
class ViewController: UIViewController {
    pravate let notificationCenter = NotificationCenter.default

    override func viewDidLoad() {
        super.viewDidLoad()
        notificationCenter.addObserver(self, selector: #selector(loginSuccess(_:)), name: .loginSuccess, object: nil)
    }
    // 사용자 세부 정보 받기
    @objc func loginSuccess(_ notification: Notification) {
        print(notification.object as [String: Any] ?? [:])
    }
    // Notification 제거
    deinit {
        notificationCenter.removeObserver(self, name: .loginSuccess, object: nil)
    }
}

class LoginManager: NSObject {
    private let notificationCenter = NotificationCenter.default

    func loginWith(_ loginDetails: [String: Any]) {
        // 함수 구현....
        notificationCenter.post(name: .loginSuccess, object: loginResponse)
    }
}
```

> Objuct와 UserInfo를 동시에 보내는 방법. (차이점을 명확하게 확인 할 수 있다.)

```swift
@objc func loginSuccess(_ notification: Notification) {
    print(notification.object as? [String: Any] ?? [:])
    print(notification.userInfo?["userInfo"] as? [String: Any] ?? [:])
}
```

---
title: "재귀함수 (반복문과 비교)"
excerpt: ""

categories:
  - swift
tags:
  - 재귀함수
last_modified_at: 2021-03-06
---

# 재귀함수

미션에 대한 PR을 보내고 리뷰어님께서 코드 리뷰를 한 내용중

<img width="413" alt="스크린샷 2021-03-06 오후 8 33 27" src="https://user-images.githubusercontent.com/70311145/110205475-6bf2f200-7ebb-11eb-9fd7-53fc871b1ca4.png">

재귀 함수라는 용어를 말씀해주셨다~

음,,, 나는 그냥 코딩하면서 함수를 재호출 한거 밖에 없는대,,?

그래서 찾아보았다☺️

---

## 재귀 함수와 반복문의 차이(비교)

재귀? 본디의 곳으로 돌아오는 것.

CS에서의 재귀는 자신을 정의할 때 자기 자신을 **재 참조**하는 방법을 뜻함.

재귀 함수(호출)은 하나의 함수가 자신을 다시 호출하여 반복되는 작업을 수행하는 함수이다.

```swift
func compare() {
    var num: Int = 1
    var number: Int = 2

    if num == number {
        print("\(num)과 \(number)는 같다.")
    } else if num > number {
        print("\(num)은 \(number)보다 크다.")
    } else {
        print("\(num)은 \(number)보다 작다.")
        compare() // <- 이게 재귀 함수 (반복과 같은 역할)
    }
}
```

### 반복?? 반복문 for문, while문이 있는데 왜??

- 재귀함수를 사용하면 코드의 가독성이 좋아진다.

  사용하는 변수의 개수도 줄어들고 구현이 반복문보다 간단하기 때문에

  빠르고 단순하게 접근할 수 있다.

  그럼 무조건 재귀함수가 더 좋은가??

- 재귀함수의 치명적인 단점으로는 스택 메모리를 사용하는 재귀의 깊이가 깊어졌을 때,

  Stack Overflow가 발생하면서 앱이 크래시가 발생할 수 있다.

  개발자는 언제나 안전한 프로그램을 개발해야하는 입장에서

  이러한 에러가 발생하는 여지를 남겨놓는 것은 바람직하지 않다.

  또 함수가 호출되고 종료될 때 **스택 프레임을 구성하고 해제하는 과정**이

  반복문보다 오버헤드가 들기 때문에 속도도 훨씬 느려지가 된다.

### 오버헤드(Overhead)

- 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간, 메모리 등을 말함.

### 결론

- 컴퓨터의 사양이 낮았을적 (하드웨어 측면)에는 반복문을 통한

  스택 오버플로우에 대비하는 방법이 당연했지만,

  시간이 지날수록 하드웨어의 성능이 발전하면서 협업이 강조되는 요즘,

  코드의 가독성을 위해 재귀함수도 충분히 고려해볼만 하다!

- 뒤늦게 알아본 사실 & 다음 공부 내용

**꼬리재귀**를 사용하면 메모리와 성능 두마리 토끼를 다 잡을 수 있다고 한다!

**꼬리 재귀?**

재귀 함수를 호출할 때 스택을 재사용하면서 메모리를 과도하게 사용하지 않도록 최적화 하는 방법

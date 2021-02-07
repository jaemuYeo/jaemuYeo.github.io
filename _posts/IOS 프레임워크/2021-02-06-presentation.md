---
title: "UIKit) Presentation"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-06

last_modified_at: 2021-02-06
---

Presentation 알아보기

이 글의 전반적인 내용은 [KXCoding](https://kxcoding.com/)을 참고하였습니다.

---

# [View Controller Presentation](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/PresentingaViewController.html)

## Presentation

뷰 컨트롤러로 구현한 UI를 화면에 표시하는 방법은 두가지가 있다.

컨테이너 뷰컨트롤러에 포함하거나 표시하는 것이 있고

화면에 직접 표시하는 Presentation 방법이 있다.

<img width="566" alt="스크린샷 2021-02-07 오후 3 24 39" src="https://user-images.githubusercontent.com/70311145/107138591-a159fd80-6958-11eb-91b3-aed52bc44f3a.png">

뷰 컨트롤러를 제공하는 것은 화면에 새 콘텐츠를 애니메이션하는 빠르고 쉬운 방법이다.

UIKit에 내장 된 프리젠 테이션을 사용하면 내장 또는 사용자 정의

애니메이션을 사용하여 새로운 뷰 컨트롤러를 표시 할 수 있다.

코드 방식 또는 segue를 사용하여 뷰 컨트롤러의 프레젠테이션을 시작할 수 있다.

UIViewController는 프레젠테이션에 필요한 모든 기능을 제공한다.

- Presentation API
- Dismissal API
- Presentation Style API
- Transition Style API

별다른 속성없이 기본값을 그대로 사용하면 새로운 화면이 모달 방식으로 표시된다.

뷰 컨트롤러가 뷰 컨트롤러를 표시하면 새로운 관계가 형성된다.

새로운 화면은 Presented VC가 되고, 그 화면을 표시하는 것은 Presenting VC가 된다.

<img width="582" alt="스크린샷 2021-02-07 오후 3 34 01" src="https://user-images.githubusercontent.com/70311145/107138802-edf20880-6959-11eb-9411-f1ed3f2a3446.png">

Presented가 차지하는 프레임은 Presentation Context가 결정한다.

프레젠테이션이 시작되면 VC계층을 따라올라가면서 Presentation Context로 지정되어있는 VC를 검색한다.

대부분 Navigation같은 컨트롤러가 Presentation Context로 지정된다.

Presentation Context로 지정된 VC가 존재하지 않는다면 최종적으로 Root VC가 사용된다.

Presentation Context는 새로운 화면을 표시할 프레임을 제공하고

Presented VC는 이 프레임에 표시된다.

<img width="545" alt="스크린샷 2021-02-07 오후 3 39 13" src="https://user-images.githubusercontent.com/70311145/107138882-a61fb100-695a-11eb-978c-7f9d06af7876.png">

스토리보드에서 Present를 연결할 때에는 세그에서 Present Modally를 사용하고

다시 화면을 되돌아갈 때에는 버튼을 통해 Dismiss가 된다.

<img width="768" alt="스크린샷 2021-02-07 오후 4 00 38" src="https://user-images.githubusercontent.com/70311145/107139432-68248c00-695e-11eb-89c1-e54fb82068d6.png">

![ezgif com-gif-maker (3)](https://user-images.githubusercontent.com/70311145/107139396-33b0d000-695e-11eb-8a72-853f2791e67c.gif)

Presentation의 스타일은 Presentation Context가 제공하는 프레임 내에서

Presented VC를 표시하는 방법을 설정한다.

<img width="258" alt="스크린샷 2021-02-07 오후 4 01 08" src="https://user-images.githubusercontent.com/70311145/107139434-6b1f7c80-695e-11eb-831e-112ae0a0025a.png">

코드를 이용하여 Presentation을 구현할 때에는 스토리보드 ID를 사용한다.

identifier를 통해 Present할 스토리보드를 선택해주고,

present(animated:completion:) 메서드를 사용하면 된다.

<img width="817" alt="스크린샷 2021-02-07 오후 4 15 20" src="https://user-images.githubusercontent.com/70311145/107139593-b9814b00-695f-11eb-8229-14218efe8005.png">

present로 이동한 화면은 dismiss(animated:completion:) 메서드로 제거한다.

<img width="465" alt="스크린샷 2021-02-07 오후 4 15 26" src="https://user-images.githubusercontent.com/70311145/107139595-bbe3a500-695f-11eb-8e28-a5675712d430.png">

---

## Present Transition Style

- Cover Vertical - 기본 효과 밑에서 위로 모달방식

- Flip Horizontal - 뒤집는 효과

- Cross Dissolve - 페이드 효과

- Partial Curl - 페이지를 넘기듯한 효과 (풀 스크린에서만 사용가능, 모달방식 사용불가)

UIModalTransitionStyle 열거형을 통해 Transition을 적용

![스크린샷 2021-02-07 오후 5 34 59](https://user-images.githubusercontent.com/70311145/107141243-d40cf180-696a-11eb-8f08-9ab5582c932c.png)

---

## Custom Presentation

VC에 화면을 표시하는 것은 Presentation Controller러가 담당한다.

이 컨트롤러는 Presented Controller가 dismiss되기 전까지 VC를 관리한다.

Presented Controller는 presented VC를 표시할 프레임을 설정하고, Transition 애니메이션을 실행한다.

Transition 과정에 추가되는 커스텀 뷰를 관리하는 것도 Presentation Controller의 역할이다.

Presentation Controller는 **UIPresentationController**로 구현되어있다.

Custom Presentation을 구현할 때에는 UIPresentationController를 서브클래싱하고,

Transitioning Delegate를 구현한다.

Presentation은 세단계로 시작한다.

<img width="227" alt="스크린샷 2021-02-07 오후 5 50 39" src="https://user-images.githubusercontent.com/70311145/107141577-04558f80-696d-11eb-9b41-2565a9fc8ae1.png">

### Presentation 단계

Transition이 시작되고 새로운 화면이 표시되는 단계이다.

Transitioning Delegate에게 커스텀 프레젠테이션 컨트롤러를 요청하고

Delegate에서 컨트롤러를 리턴하면 커스텀 프레젠테이션이 시작된다.

- PresentationTRansitionWillBegin() - Transition에 추가되는 커스텀 뷰를 추가하고 애니메이션에 필요한 속성을 설정하는 코드를 구현

이어서 Transition이 실행된 후에 화면이 전환된다.

Transition이 실행되는 동안 프레젠테이션 컨트롤러에서 아래 두 메서드가 연달아 호출된다.

- ContainerViewWillLaoutSubviews() - Transition에 사용되는 커스텀 뷰 배치를 구현

- ContainerViewDidLayoutSubviews() - Transition에 사용되는 커스텀 뷰 배치를 구현

트렌지션이 완료된 후에는 아래 메서드가 호출된다.

- PresentationTransitionDidEnd()

여기까지 구현된 후 Presentation 단계가 종료되고 Management 단계로 전환된다.

### Management

Management에서는 디바이스 회전과 같은 이벤트를 처리한다.

프레임의 크기가 업데이트되면 트렌지션 컨트롤러에서 아래 메서드가 호출된다.

- viewWillTransition(to:with:)

오토레이아웃을 구현했다면 Management단계에서 처리해야할 대부분의 작업이 자동으로 처리된다.

오토레이아웃이 되어있지 않은 뷰가 추가되어있다면 프레임을 직접 업데이트 해야한다.

### Dismissal

Presented VC를 닫으면 Dismissal 단계가 시작된다.

- dismissalTransitionWillBegin() - 호출되고나서 Transition이 실행된다.

애니메이션이 실행되는 동안 아래 두 메서드가 연달아서 호출된다.

- containerViewWillLayoutSubviews()

- containerViewDidLaoutSubviews()

Transition이 완료되면 아래 메서드가 호출된다.

- dismissalTransitionDidEnd()

---
title: "UIKit) Alert으로 로그인 화면 구현해보기"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-10

last_modified_at: 2021-01-10T08:06:00-21:00
---

# Alert Controller & Adding Text Field

앱스토어처럼 별도의 로그인 화면도 구현되어있지만

Alert를 통해 로그인을 구현하는 창이 뜨기도 한다.

디자인을 고려할 필요가 없다면 이렇게 구현하기도 한다.

Alert에 Text Field를 추가해서 구현한다.

<img width="496" alt="스크린샷 2021-01-10 오후 6 29 01" src="https://user-images.githubusercontent.com/70311145/104119310-c8310e00-5371-11eb-8170-485d6cd6bd0b.png">

버튼을 클릭하면 textField가 추가된 창을 표시하고

창에서 값을 입력 후 확인버튼을 누르면 두개의 레이블에 입력한 값을 표시해보자.

<img width="1064" alt="스크린샷 2021-01-10 오후 6 33 18" src="https://user-images.githubusercontent.com/70311145/104119650-2ced6800-5374-11eb-933f-019e9e7b3580.png">

두개의 Label과 Button을 각각 아웃렛 액션으로 연결해준다.

<img width="854" alt="스크린샷 2021-01-10 오후 6 49 44" src="https://user-images.githubusercontent.com/70311145/104119708-9ff6de80-5374-11eb-9278-5061676b40ce.png">

UIAlertController메서드를 사용한 인스턴스를 만들어주고

textField를 두개 추가하였다.

Text Field를 컨트롤러에 추가하려면 addTextField를 사용한다.

<img width="378" alt="스크린샷 2021-01-10 오후 6 35 19" src="https://user-images.githubusercontent.com/70311145/104119734-e8160100-5374-11eb-8789-f9d04f1ecfba.png">

<img width="370" alt="스크린샷 2021-01-10 오후 6 35 37" src="https://user-images.githubusercontent.com/70311145/104119736-e9dfc480-5374-11eb-9df5-6751d7fecd73.png">

파라미터로 클로저를 전달하는데 클로저에는 UITextField가 파라미터로 전달된다.

다음으로 확인과 취소 액션을 구현해보자.

<img width="739" alt="스크린샷 2021-01-10 오후 6 54 19" src="https://user-images.githubusercontent.com/70311145/104119777-480ca780-5375-11eb-8b05-daca71eea2e9.png">

okAction 부분을 보면

<img width="331" alt="스크린샷 2021-01-10 오후 6 56 36" src="https://user-images.githubusercontent.com/70311145/104119853-d2eda200-5375-11eb-8ad7-fdb14266253a.png">

textFields 속성을 통해 앞에서 추가한 Text Field에 접근한다.

이 곳에는 TExt Field가 추가된 순서대로 저장되어 있다.

<img width="346" alt="스크린샷 2021-01-10 오후 6 57 42" src="https://user-images.githubusercontent.com/70311145/104119855-d54ffc00-5375-11eb-9873-b51d8cdaa9a3.png">

첫번째 Text Field에 접근한 다음에 입력되어있는 값을 Label에 표시한다.

보통 배열에 접근할 때에 index를 사용하지만 first 속성으로 접근하게 되면

배열이 비어있는 경우에 오류가 발생하지 않아 조금 더 안전하다.

다음은 두번째 Text Field에 접근하는 방법을 구현한다.

<img width="453" alt="스크린샷 2021-01-10 오후 6 57 15" src="https://user-images.githubusercontent.com/70311145/104119854-d4b76580-5375-11eb-9512-8824a616aa61.png">

첫번째 Text Field에서 first 속성을 접근한 것처럼 이번에는 마지막 배열에 접근한다.

<img width="562" alt="스크린샷 2021-01-10 오후 7 06 00" src="https://user-images.githubusercontent.com/70311145/104120007-ec431e00-5376-11eb-9b39-1e1adc545d54.png">

오!! 어디서 많이 봤던 화면과 액션을 통한 Label의 변경이 잘 구현되었다.

하지만 뭔가 아쉬운게 있다.

TextField에 플레이스 홀더와 password 입력시 마스킹이 되면 조금 더 완벽해질 것 같다.

<img width="335" alt="스크린샷 2021-01-10 오후 7 10 51" src="https://user-images.githubusercontent.com/70311145/104120122-beaaa480-5377-11eb-9d85-f88486f34bdf.png">
<img width="375" alt="스크린샷 2021-01-10 오후 7 12 03" src="https://user-images.githubusercontent.com/70311145/104120123-bfdbd180-5377-11eb-9c80-f6efd9173600.png">

이 메서드의 전달하는 클로저에서 각각의 Text Field를 원하는 속성으로 구성 할 수 있다.

즉, 클로저에서 파라미터로 접근해서 원하는 것을 구성할 수 있게 된다.

<img width="384" alt="스크린샷 2021-01-10 오후 7 15 14" src="https://user-images.githubusercontent.com/70311145/104120181-324cb180-5378-11eb-817c-4905ea881120.png">

각각의 Text Field의 Placeholder 속성과 Text Entry 속성을 설정해주면 끝난다.

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/70311145/104120246-8fe0fe00-5378-11eb-9519-6d2a9f48b75e.gif)

---

참고 자료 - [KXCoding](https://kxcoding.com/)

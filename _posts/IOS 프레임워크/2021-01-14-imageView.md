---
title: "UIKit) Image View"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-14

last_modified_at: 2021-01-14
---

# UIImageView 알아보기

## Image View

인터페이스에서 단일 이미지 또는 일련의 애니메이션 이미지를 표시하는 개체이다.

<img width="677" alt="스크린샷 2021-01-14 오후 3 25 44" src="https://user-images.githubusercontent.com/70311145/104555086-9de89480-5680-11eb-96ed-6626070dc47d.png">

Image View는 종횡비를 유지하면서 프레임내부에 꽉 채워서 표시한다.

image는 종횡비가 중요한 요소이기때문에 특별한 이유가 없다면

Content Mode에서 Aspect Fit 또는 Aspect Fill을 사용한다.

---

**Content Mode**

모드의 이름들이 직관적이라 영상으로보면 쉽게 알 수 있다.

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/70311145/104556668-56afd300-5683-11eb-9176-0813a29041a1.gif)

- Scale To Fill
- Aspect Fit
- Aspect Fill
- Redraw
- Center
- Top
- Bottom
- Left
- Right
- Top Left
- Top Right
- Bottom Left
- Bottom Right

Content Mode가 Aspect Fill인 상태에서 Drawing속성의 Clips to Bounds가

체크되어있으면 설정된 ImageView크기에 맞게 설정되지만 체크가 해제되어있으면

<img width="258" alt="스크린샷 2021-01-14 오후 4 32 02" src="https://user-images.githubusercontent.com/70311145/104558407-169e1f80-5686-11eb-8ea7-d25aa8716a09.png">

<img width="370" alt="스크린샷 2021-01-14 오후 4 17 25" src="https://user-images.githubusercontent.com/70311145/104557119-07b66d80-5684-11eb-9d3f-bd719e4583a9.png">

위에처럼 imageVIew의 크기보다 벗어난 범위에서 설정된 image의 전체를 인터페이스에 보여준다.

---

Tip!

이미지를 텍스트와 데이터를 비교했을때 이미지가 상당히 큰 데이터를 차지한다.

가능하다면 imageView의 크기와 같거나 유사한 크기의 이미지를 사용하는것이 바람직하다.

imageView의 크기와 이미지의 크기가 같다면 불필요한 확대나 축소가 필요없기 때문에

성능상의 이점이 있다.

---

**State**

ImageView는 상태에 따라 두가지의 이미지를 가질 수 있다.

<img width="131" alt="스크린샷 2021-01-14 오후 4 33 27" src="https://user-images.githubusercontent.com/70311145/104558508-40574680-5686-11eb-973d-7c8865a68851.png">

highlighted에 이미지를 추가하고 State의 Hightlighted를 체크하면

Hightlighted 상태의 이미지가 보여진다.

조건에 따라서 이미지를 토글해야할때 자주사용하는 패턴이다.

이미지를 바꾸는 것 보다 highlihgted 상태를 바꾸는 것이 더 심플하다!

---

**constraints**

제약을 추가하게 되면 imageView는 이미지의 실제크기로 업데이트 된다.

Image View는 **Intrinsic Content Size**를 가지고 있다.

이 값은 imageView에 이미지가 설정되어 있는 경우에만 사용된다.

imageView는 표시하고있는 이미지를 통해 크기를 판단하는데

이미지가 없다면 Intrinsic Content Size를 알 수 없다.

그래서 이미지가 없을 때 제약을 추가하게 되면 오류가 난다.

대부분의 경우에는 imageView의 크기를 직접 지정하고 위에서 알아본

Content Mode를 적절한 방법으로 사용하면서 구현하는 것을 추천한다.

---

**Image Animation**

Image View에서 .Jpg나 .png같은 이미지는 제공하지만 .gif같은 이미지는 제공하지 않는다.

하지만 이미지 시퀀스를 사용하면 .gif 같은 느낌의 애니메이션효과를 구현할 수 있다.

- 이미지 시퀀스에 포함된 모든 이미지는 사이즈와 스케일펙터가 동일해야 한다.

 <img width="454" alt="스크린샷 2021-01-14 오후 4 53 24" src="https://user-images.githubusercontent.com/70311145/104560321-0e93af00-5689-11eb-8e2c-ccb8a5a55ba3.png">

imageView는 animationImages라는 속성을 가지고 있다.

animationImages 속성에 이미지의 배열을 저장해두고 startAnimating()메서드를 호출하면 된다.

<img width="442" alt="스크린샷 2021-01-14 오후 4 53 27" src="https://user-images.githubusercontent.com/70311145/104560332-12273600-5689-11eb-894d-f872d17fb343.png">

Start가 있으면 반대로 Stop도 있다.

stopAnimating을 구현 할때에는 상태를 확인 후 구현하는 것이 좋다.

<img width="432" alt="스크린샷 2021-01-14 오후 4 55 55" src="https://user-images.githubusercontent.com/70311145/104560564-67634780-5689-11eb-9a3f-fb3e61272cc5.png">

isAnimating()을 통해 상태를 확인 후 stopAnimating()을 호출하였다.

![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/70311145/104560980-0425e500-568a-11eb-8a2f-5f5d3b95bb92.gif)

앱을 실행하면 이미지가 뜨지않고 Start 버튼을 누르면 이미자가 뜨면서

배열에 지장된 이미지들이 애니메이션적용되서 보여진다.

그리고 Stop버튼을 누르면 애니메이션이 끝나고 이미지가 사라진다.

앱실행과 동시에 이미지가 보이려면 Place Holder를 같이 설정해줘야한다.

<img width="137" alt="스크린샷 2021-01-14 오후 5 03 54" src="https://user-images.githubusercontent.com/70311145/104562114-41d73d80-568b-11eb-82fc-601d9efbee64.png">

애니메이션시간을 설정할 때에는 animationDuration 속성을 사용하고

animationDuration의 값을 0.0으로 설정하면 기본값으로 설정한다.

animationDuration의 값으 1.0으로 주면 1초의 애니메이션 시간이 정해지고

배열에 네가지의 이미지가 있으므로 한 인덱스당 0.25초로 보여진다.

애니메이션의 반복횟수를 설정할 때에는 animationRepeatCount속성을 사용하고

animationRepeatCount의 기본값은 0이다. 기본값 설정 시 애니메이션이 무한정 반복한다.

<img width="395" alt="스크린샷 2021-01-14 오후 5 08 43" src="https://user-images.githubusercontent.com/70311145/104562118-43086a80-568b-11eb-8baa-e09b5e784e48.png">

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/104562275-7b0fad80-568b-11eb-8b75-18c502eae789.gif)

---

## Image

IOS 프로젝트에서는 PNG와 JPG 이미지파일을 사용한다.

> 애플은 PNG를 사용하라고 권장하고 있다.

[HIG의 이미지 관련내용](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/image-size-and-resolution/)

이미지를 추가할 때에는 프로젝트 내에 Assets 폴더에서 관리한다.

<img width="190" alt="스크린샷 2021-01-14 오후 5 19 14" src="https://user-images.githubusercontent.com/70311145/104563158-a5159f80-568c-11eb-8b71-a2d6c40a00c8.png">

이미지를 드래그해서 올리게 되면 오른쪽에 Image Set이 표시된다.

<img width="381" alt="스크린샷 2021-01-14 오후 5 25 04" src="https://user-images.githubusercontent.com/70311145/104563792-764bf900-568d-11eb-9ada-d14065444d0d.png">

이미지 셋에는 1x 2x 3x 가 있다.

- 1x - 레티나 디스플레이가 없는 예전 디바이스에서 사용 (요즘은 사용 x)
- 2x - 일반적인 레티나 디스플레이를 탑제한 디바이스에서 사용
- 3x - ios 기기에 plus나 max가 붙은 고해상도의 디바이스에서 사용

기본적으로 이미지를 추가하면 1x로 추가되고 드래그를 통해 다른 스케일로 이동 가능하다.

바로 원하는 스케일로 이동하고싶다면 이미지파일 이름 뒤에 접미어를 붙여야 한다.

이미지의 이름이 apple.png이라고 가정하면

> apple.png , apple@2x.png, apple@3x.png

assets 파일에 저장된 이미지의 이름은 프로젝트 내에서 이미지를 대표하는 이름으로 사용되므로

단순하고 직관적인 이름으로 사용하기를 권장한다.

---

코드를 통해 이미지를 표시할 때에는 UIImage 클래스를 사용한다.

<img width="376" alt="스크린샷 2021-01-14 오후 5 42 33" src="https://user-images.githubusercontent.com/70311145/104565678-f4110400-568f-11eb-9f9d-6d754a405ae9.png">

<img width="376" alt="스크린샷 2021-01-14 오후 5 42 49" src="https://user-images.githubusercontent.com/70311145/104565683-f6735e00-568f-11eb-8073-cc4f8255df41.png">

```swift
UIImage(named:)   // assets 파일에 저장된 이미지를 사용할 때
UIImage(systemName:) // 애플이 제공하는 기본 이미지를 사용할 때
```

이미지의 이름을 입력할 때에는 String 타입이고 대소문자를 모두 구분해서 정확히 입력해야 한다.

Image Leteral 을 사용하게되면 코드에서 눈으로 직접 확인할 수 있어

어떤 이미지를 사용하는지 바로 확인 할 수 있지만 xcode버전에 따라서 동작이 안돼거나

지원을 안하는 경우도 있다. 그리고 assets파일에서 해당 이미지가 삭제되거나 이름이 변경되었을 때에

UIImage클래스를 통해 구현했을 때에는 nil을 리턴하지만

이미지 리터럴의 경우에는 에러가 나고 앱이 종료될 수도 있다.

<img width="576" alt="스크린샷 2021-01-14 오후 6 03 47" src="https://user-images.githubusercontent.com/70311145/104568096-f45ece80-5692-11eb-90fd-a11e184d9ca8.png">

viewDidLoad()에 이 코드를 작성하면 이미지가 구현된다.

---

**Image의 크기를 코드로 확인하는 방법**

이미지의 크기를 확인할 때에는 size 속성에 접근하는데 이미지의 크기를 픽셀이 아닌

포인트 단위로 리턴한다.

<img width="295" alt="스크린샷 2021-01-14 오후 6 09 33" src="https://user-images.githubusercontent.com/70311145/104568859-ef4e4f00-5693-11eb-8f6d-bea8ddf76e96.png">

만약 픽셀 단위의 크기를 얻고싶다면 size 속성이 리턴한 값에 scale 속성의 값을 곱해야 한다.

<img width="672" alt="스크린샷 2021-01-14 오후 6 11 23" src="https://user-images.githubusercontent.com/70311145/104568867-f1181280-5693-11eb-9f56-34fc5641fe24.png">

이미지를 네트워크를 통해 다른곳으로 전송하거나 파일에 저장할 때에는

바이너리 형태로 바꿔야 한다.

<img width="439" alt="스크린샷 2021-01-14 오후 6 14 23" src="https://user-images.githubusercontent.com/70311145/104569715-5f5cd500-5694-11eb-91d9-dd912ae8478d.png">

jpegDate를 저장할 때에는 압축비율의 값을 0.0 ~ 1.0 의 값을 파라미터로 전달해야 한다.

<img width="750" alt="스크린샷 2021-01-14 오후 6 23 08" src="https://user-images.githubusercontent.com/70311145/104570692-9aabd380-5695-11eb-810e-6ba18637d1b2.png">

<img width="777" alt="스크린샷 2021-01-14 오후 6 22 54" src="https://user-images.githubusercontent.com/70311145/104570679-97b0e300-5695-11eb-8a36-7d406ff8aa7f.png">

---

## Vector Image

이미지를 추가할때 이미지크기를 늘리게되면 출력품질이 낮아지는 것을 볼 수 있다.

다양한 크기의 이미지를 여러개 사용해서 문제를 해결할 수 있지만

이러한 문제를 해결하기 위해서 vector image를 사용하게 되면 이미지 하나로 해결가능하다.

vector image는 점과 점을 연결해 수학적 원리로 그림을 그려 표현하는 방식을 말한다.

vector image는 이미지를 수학적으로 계산해서 그리기 때문에 scale 별로 따로 추가하지 않아도 된다.

svg 파일이나 pdf파일이 대표적인 예이다.

pdf벡터 이미지는 xcode 6부터 도입 되었고 지금은 거의 모든 버젼에서 사용가능하다.

호완성은 좋으나 이미지를 pdf벡터 이미지로 바꾸는 것이 번거롭다.

svg이미지는 xcode12와 ios13버젼부터 지원한다. 그래서 배포버젼에 따라 사용이 불가능 할 수 있다.

하지만 svg 자체가 웹개발에서는 이마 많이 사용중이고 파일 포맷으로 인한 문제는 거의 없다.

배포버전이 ios13이상이라면 svg를 추천하고 그보다 낮다면 pdf벡터이미지를 사용하는 것이 좋다.

벡터 이미지를 사용 할 때에는 assets파일에서 이미지의 속성을 바꿔야한다.

<img width="136" alt="스크린샷 2021-01-14 오후 6 51 20" src="https://user-images.githubusercontent.com/70311145/104576213-3f7cdf80-569b-11eb-9e21-8c4e4ad7be42.png">

벡터이미지를 추가하였다면 오른쪽 속성에서 Preserve Vector Data를 체크해주고

Scales옵션을 Single Scale로 바꿔주면 벡터이미지가 추가된다.

---

## Template Image

> Template Image - 원본 이미지에서 컬러정보를 모두 제거하고 불투명한 부분을 TintColor로 채운 이미지이다.

보통의 이미지를 나타내는 Button의 백그라운드 이미지나 ImageView의 이미지는 원본을

그대로 표시하는 반면 bar button item은 Template Image로 표시된다.

원본이미지를 표시하고 싶다면 assets 파일의 속성을 변경하면 된다.

<img width="469" alt="스크린샷 2021-01-14 오후 7 25 20" src="https://user-images.githubusercontent.com/70311145/104578619-4b1dd580-569e-11eb-872e-dc7b372026d3.png">

속성중 Render As를 클릭하면 세가지 옵션이 뜬다.

<img width="247" alt="스크린샷 2021-01-14 오후 7 25 24" src="https://user-images.githubusercontent.com/70311145/104578626-4ce79900-569e-11eb-8169-7133f5c3e385.png">

여기서 Original Image를 선택하게되면 어디서든 원본 이미지를 사용하게 된다.

코드를 통해서 Template Image를 적용해보자.

Tint Color를 사용하는 이유는 Tint Color를 통해서 앱의 컬러테마를 쉽게 바꿀 수 있기때문이다.

UIImage클래스에 withRenderingMode메서드를 이용해 모드를 전달할 수 있다.

<img width="363" alt="스크린샷 2021-01-14 오후 7 31 50" src="https://user-images.githubusercontent.com/70311145/104579789-c9c74280-569f-11eb-97ca-9beee798cad2.png">

모드에는 위에서 보았던 assets파일의 속성에서 보았던 세가지속성을 선택 할 수 있다.

<img width="376" alt="스크린샷 2021-01-14 오후 7 31 59" src="https://user-images.githubusercontent.com/70311145/104579798-cb910600-569f-11eb-8487-d89e9b4aad4f.png">

Tint Color의 속성은 모든 subView에 상속된다.

이 특징을 잘 활용해 Tint Color와 Template Image를 조합해 컬러테마를 쉽게 구현할 수 있다.

<img width="751" alt="스크린샷 2021-01-14 오후 7 36 14" src="https://user-images.githubusercontent.com/70311145/104579801-cc299c80-569f-11eb-9a08-92885971b7a8.png">

---

## Image Resizing

<img width="310" alt="스크린샷 2021-01-14 오후 8 19 13" src="https://user-images.githubusercontent.com/70311145/104584345-cdf65e80-56a5-11eb-94cb-10fa6b2cfd11.png">

위 사진에서 imageView의 프레임은 RootView의 프레임과 같다.

대용량 픽셀의 사진을 사용하였고 Content Mode가 center로 지정되어있어

사진의 중앙을 중심으로 이미지를 보여주고 있다.

Resizing을 이용하여 전체이미지가 imageView프레임안에 모두 들어오도록 구현할 수 있다.

<img width="981" alt="스크린샷 2021-01-14 오후 8 52 54" src="https://user-images.githubusercontent.com/70311145/104587623-845c4280-56aa-11eb-9291-b09a4e1050c7.png">

extension을 통해 imageContext를 사용한다.

resizingWithImageContext메서드는 리사이징 할 이미지와 리사이징 할 크기를 파라미터로 받은 후

imageContext를 생성하는 메서드를 구현한다.

<img width="593" alt="스크린샷 2021-01-14 오후 8 30 06" src="https://user-images.githubusercontent.com/70311145/104585890-0eef7280-56a8-11eb-8916-7d36facd4d79.png">

위 메서드는 무언가를 그릴 수 있는 그림판을 만드는 역할이다.

첫번 째 파라미터로 크기를 전달한다.

두번 째 파라미터는 사진에 투명한 부분이 있다면 false 없다면 true를 전달한다.

세번 째 파라미터는 이미지의 scale을 전달한다. 0.0은 디바이스의 스케일을 그대로 사용한다.

<img width="461" alt="스크린샷 2021-01-14 오후 8 36 19" src="https://user-images.githubusercontent.com/70311145/104585976-30505e80-56a8-11eb-8325-c13fa11aca48.png">

이렇게 구현하면 그림판이 만들어 졌고 이미지나 텍스트를 자유롭게 구현할 수 있다.

draw(in:)메서드를 사용해 이미지를 프레임 내부에 그려보도록 하자.

<img width="467" alt="스크린샷 2021-01-14 오후 8 39 41" src="https://user-images.githubusercontent.com/70311145/104586303-a5bc2f00-56a8-11eb-9d9d-db0ec7b776c3.png">

이렇게 구현하면 원본이미지가 지정 된 프레임 내에 축소되어서 나타난다.

그 다음에는 context에 그려져 있는 이미지를 실제 이미지로 바꿔줘야 한다.

<img width="503" alt="스크린샷 2021-01-14 오후 8 42 09" src="https://user-images.githubusercontent.com/70311145/104586691-2418d100-56a9-11eb-8949-f6ea99af05a0.png">

현재 사용중인 image context에서 이미지를 가져오는 함수이다.

context에서 작업이 완료되면 반드시 context를 해제해야 한다.

<img width="226" alt="스크린샷 2021-01-14 오후 8 45 16" src="https://user-images.githubusercontent.com/70311145/104586867-6cd08a00-56a9-11eb-93dd-cd40bf12c8cb.png">

이렇게 하면 정상적으로 해지되었고 viewDidLoad에서 축소할 이미지와 축소할 크기를 선언해 줘야한다.

<img width="812" alt="스크린샷 2021-01-14 오후 8 50 53" src="https://user-images.githubusercontent.com/70311145/104587446-465f1e80-56aa-11eb-83c6-93f3754bb683.png">

<img width="1147" alt="스크린샷 2021-01-14 오후 8 49 18" src="https://user-images.githubusercontent.com/70311145/104587434-4101d400-56aa-11eb-93c3-1c50665101cf.png">

코드구현을 마치면 앱 실행시 이미지가 축소되어서 표시된다.

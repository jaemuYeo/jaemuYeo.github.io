---
title: "UIKit) Page Control로 간단한 앨범만들기"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-08

last_modified_at: 2021-01-08
---

# Page Control로 사진앱 만들기

> 프로젝트 이미지 파일 추가 ( images 그룹을 만들고 추가 )

<img width="272" alt="스크린샷 2021-01-08 오전 9 52 44" src="https://user-images.githubusercontent.com/70311145/103961201-500ef080-5197-11eb-9888-11ab60403605.png">

> 인터페이스 빌더에 ImageView와 Page Control 라이브러리 추가

<img width="587" alt="스크린샷 2021-01-08 오전 9 56 36" src="https://user-images.githubusercontent.com/70311145/103961437-d297b000-5197-11eb-8eba-92943f98d1ec.png">

> imageView와 page Control 아웃렛 추가

- imageVIew -> "collection"
- page control -> "pageControl"

<img width="867" alt="스크린샷 2021-01-08 오전 9 58 34" src="https://user-images.githubusercontent.com/70311145/103961586-23a7a400-5198-11eb-918f-0886ed6f4f83.png">

> Page Control 액션 함수 추가

- page control -> "pageChanged"

<img width="836" alt="스크린샷 2021-01-08 오전 10 01 56" src="https://user-images.githubusercontent.com/70311145/103961776-91ec6680-5198-11eb-92eb-c4aa06139ac4.png">

> 이미지 배열을 정의하고 viewDidLoad와 page control 메서드에 소스 추가

<img width="697" alt="스크린샷 2021-01-08 오전 10 16 33" src="https://user-images.githubusercontent.com/70311145/103962566-9ade3780-519a-11eb-8fa9-e5983eff16d6.png">

---

이미지가 화면에 꽉 차길 원해서 ImageView 의 속성 중 Content Mode를 "Aspect Fill"로 변경.

<img width="559" alt="스크린샷 2021-01-08 오전 10 18 47" src="https://user-images.githubusercontent.com/70311145/103962732-fd373800-519a-11eb-91f5-39ad1dbabae6.png">

<img width="559" alt="스크린샷 2021-01-08 오전 10 19 08" src="https://user-images.githubusercontent.com/70311145/103962764-0d4f1780-519b-11eb-9555-4739bf728c92.png">

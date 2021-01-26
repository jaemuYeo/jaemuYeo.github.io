---
title: "당근마켓 UI 만들어보기 (Table View & Collection View)"

categories:
  - ios

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-01-23

last_modified_at: 2021-01-23
---

# 당근마켓 클론(연습)

![ezgif com-gif-maker](https://user-images.githubusercontent.com/70311145/105827895-de8fc880-6005-11eb-8246-eebb96da1857.gif)

## 메인화면 (Table View)

<img width="945" alt="스크린샷 2021-01-26 오후 6 29 12" src="https://user-images.githubusercontent.com/70311145/105826867-99b76200-6004-11eb-8890-1bb575cebc62.png">

<img width="397" alt="스크린샷 2021-01-26 오후 6 29 18" src="https://user-images.githubusercontent.com/70311145/105826888-9fad4300-6004-11eb-8698-80464df45ccb.png">

아주 간단한 메서드로만 구현을 했다.

모델을 만들어서 더 많은 스크롤을 구현해보려했으나 아직 실력이 부족해서 구현하지 못했다.

커스텀 셀을 만들어서 셀의 UI를 만들었다.

Separator 여백을 양쪽 모두 15값을 주었고 스타일을 지정해주었다.

---

## 검색화면 (Collection View)

<img width="1101" alt="스크린샷 2021-01-26 오후 6 29 32" src="https://user-images.githubusercontent.com/70311145/105826896-a0de7000-6004-11eb-9151-f7c298a2812d.png">

<img width="941" alt="스크린샷 2021-01-26 오후 6 29 42" src="https://user-images.githubusercontent.com/70311145/105826904-a50a8d80-6004-11eb-9bf4-558d65f680b9.png">

<img width="327" alt="스크린샷 2021-01-26 오후 6 29 48" src="https://user-images.githubusercontent.com/70311145/105826907-a63bba80-6004-11eb-95ef-d8650f4163ea.png">

<img width="369" alt="스크린샷 2021-01-26 오후 6 30 01" src="https://user-images.githubusercontent.com/70311145/105826915-a8057e00-6004-11eb-9e6c-b7465798efe0.png">

컬렉션뷰도 마찬가지로 모델을 만들지 못해어 배치만 비슷하게 구현하였다.

섹션별로 다른 UI를 주고싶었지만 아직 구현하지 못했다.

스터디를 통해 셀마다 컬렉션뷰를 넣어주고 컨트롤러를 구현하는 방식도 알게되었고

검색을 통해서 컴포지션과 직교 스크롤링에 대한 방법도 알아내었다.

numberOfItemsInSection 메서드를 통해서 섹션별 셀의 갯수를 정해놨지만

추후에 레이아웃을 변경할 때 다른 방식으로 셀을 나눠보기로 할것이다.

아직은 하나의 셀만 커스텀 하였지만 셀을 나누면서 4가지 커스텀셀을 구현하여야한다.

## 개선해야 할 사항

- 컬렉션뷰 레이아웃 나누기
- 두 화면 모두 Cell prefetching, Data Prefetching 구현
- 모델구현하고 컨트롤러에 배열 지우기
- xib로 셀 불러오기

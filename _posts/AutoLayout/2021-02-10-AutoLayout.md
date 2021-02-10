---
title: "UIKit) Auto Layout"

categories:
  - AutoLayout

tags:
  - [UIKit, framework]

toc: true

toc_sticky: true

date: 2021-02-10

last_modified_at: 2021-02-10
---

# [Auto Layout](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/index.html)

오토 레이아웃은 해당 뷰에 적용된 제약 조건에 따라 뷰 계층 구조에있는 모든 뷰의 크기와 위치를 동적으로 계산한다.

지금까지 나온 모든 디바이스와 앞으로 나올 디바이스의 해상도와 스케일을 모두 암기할 필요는 없다.

오토레이아웃을 통해 제약을 추가하는 방법만 잘 알고있으면 모든 해상도에서 UI를 구현할 수 있다.

UI를 구성하는 방식에는 변화가 있다.

---

- **Frame-Based Layout**

  가장 먼저 사용된 방식이다.

  프레임의 상위 뷰에 좌표시스템에서 특정 뷰의 위치와 크기를 나타내는 용어이다.

  개발자가 프레임을 직접 제작하고 설정해야하는 방식이다.

  하나의 해상도만 존재하던 시절에는 문제가 없었지만 요즘같이 다양한 해상도가 나오면서

  프레임을 제작하는 과정이 복잡해졌다. 특히 상위 뷰의 크기변화에 따라 하위 뷰의 크기를 변경하는 작업이

  많이 어려워 졌다. 그래서 나온 방법이 Auto resizing mask이다.

  Auto resizing mask는 상위 뷰의 프레임이 변경될 때에 하위 뷰의 프레임이 변경되는

  규칙을 미리 지정된 여섯개의 비트마스크로 지정한다.

  Auto resizing mask을 통해서 프레임을 계산하는 부담은 줄었지만 모든 문제를 해결하지는 못했다.

- **Auto Layout**

  위 문제를 해결하기 위해 나온 방식이 오토 레이아웃이다.

  이 방식이 나오면서 Frame-Based Layout과 Auto resizing mask가 완전히 사라진 것은 아니다.

  오토 레이아웃에서 해결할 수 없는 약간의 문제를 위의 방식으로 해결할 수 있다.

  Auto resizing mask는 UI프로토타이핑에 활용되고 있다.

  오토 레이아웃은 UI를 구성하는 뷰의 크기나 위치를 다른 요소와의 관계를 나타내는 특별한 규칙을 통해

  자동으로 계산하고 배치하는 기술이다.

  Constraints(제약)는 오토 레이아웃에서 가장 중요한 개념이다.

  Constraints를 기반으로 최종 프레임에 뷰를 배치한다.

- **Adaptive Layout**

  IPhon 8이 나오던 2014년도에 UI구성 방식에 또 다른 방식이 등장한다.

  애플은 Adaptive Layout 통해 모든 디바이스의 해상도에 대응하는

  하나의 UI를 개발할 수 있도록 Size Class와 Trait Collection을 도입했다.

  이 전에는 아이폰과 아이패드의 스토리보드를 구분해서 개발했지만

  Adaptive Layout이 도입된 이 후 하나의 Universal Storyboard에서 개발한다.

  개발 입장에서 아이폰과 아이패드의 구분이 거의 없어졌다.

  Size Class를 통해 UI를 표시할 수 있는 영역의 크기를 큰 틀에서 구분하고,

  Trait Collection을 통해 상세한 인터페이스 환경을 구분하는 방식으로 변경되었다.

---
title:  "M1 Mac 에서 Flutter 개발환경 설정"
date:   2021-06-06 21:04:41 +0900
categories: flutter
---


1. XCode
  * App Store에서 검색하여 설치
  * 실행하여 라이센스 동의

2. Cocoapods (라이브러리 종속성 관리)
  * [링크](https://guides.cocoapods.org/using/getting-started.html#installation) 참조하거나 아래 명령어를 입력하여 설치
```shell
sudo gem install cocoapods
```

3. Intellij 설치
  * Intellij 를 사용하는 이유는 Android Studio 가 M1을 정식 지원하지 않고 로제타로 돌기 때문에 렉이 발생한다
  * [링크](https://www.jetbrains.com/ko-kr/idea/download/#section=mac)를 통하여 다운로드 & 설치
  * plugins > flutter 검색하여 plugin 설치

4. Flutter SDK 설치
  * [링크](https://flutter.dev/docs/get-started/install/macos "Flutter 설치 가이드 링크") 참조 설치
  * flutter path 설정
    1. ```shell
sudo vi /etc/paths
      ```
    2. 맥북 Password 입력
    3. 키보드 i를 입력하여 편집모드 진입
    4. 추가하고자 하는 경로 입력 (flutter/bin 위치)
    5. `ESC`누른 후 `:wq` 를 입력

5. Android studio 설치
  * [링크](https://developer.android.com/studio/archive?hl=ko) 참조하여 설치
  * 2021년도 6월 3일 기준 아직 M1 칩 대응 안됨 로제타로 작동
  * Intellij 와 동일하게 Flutter plugin 설치
  * Android sdk license 동의 (터미널에서 실행)
    1. ```flutter doctor --android-licenses```
    2. 만약 동의 안된다면 다음 링크를 참조. https://itslog.tistory.com/entry/flutter-doctor-error-Android-license-status-unknown

마지막으로 터미널에서 ```flutter doctor``` 실행 후 아래와 같이 나온다면 성공.
![flutter doctor 실행 결과](/assets/images/2021/06/20210606_01.png "flutter doctor 실행 결과")

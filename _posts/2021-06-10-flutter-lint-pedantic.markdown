---
title:  "[pedantic]Flutter Code 를 깔끔하게"
date:   2021-06-10 15:52:00 +0900
categories: flutter
---


## 왜 pedantic 인가
### 새로 입사한 회사의 코드 품질이 좋지 않다

최근 새로운 회사에 입사하였다.

이 회사는 Flutter 로 앱을 개발하고 있었고, 이미 베타버전까지 완성된 상태이다.

많은 스타트업 or 중소기업이 겪는 문제일꺼라 생각하지만 노하우와 리소스 부족으로 코드품질이 좋지 못하다.

물론 여기서 난 리소스가 부족하던 풍족하던 무조건 clean code 를 작성해야하며, 언어의 표준 code convention을 준수하여아 한다고 강력하게 믿는다.

__사실 리소스가 부족할 수록 지켜져야 하는게 clean code 와 code convention 이다.__

수십만 라인의 코드를 혼자 리팩토링 할 수도 없고, code convention 문서를 공유한다고 해도 잘 지키고 있는 지 매번 감시할 수도 없다.

그러하여 자동으로 검사하여 경고메시지 or 에러메시지를 출력해주는 Code linter가 필요하게 되었고, 검토중 pedantic이 가장 적합하다 판단했다.

## pedantic 설치

![영어사전 의미](/assets/images/2021/06/20210610_06.png "사전적의미")

[Pub 홈페이지](https://pub.dev/packages/pedantic)

pubspec.yaml 에 아래 코드 추가

```yaml
dev_dependencies:
  pedantic: ^1.11.0
```

analysis_options.yaml 을 프로젝트 root에 작성 (pubspec.yaml 과 같은 레벨)
```yaml
include: package:pedantic/analysis_options.yaml
```

터미널에서 아래 명령어 실행
```shell
flutter pub get
```

이렇게 간단한 작업만으로 Code linter 설정이 가능하다.

결과 ...

![영어사전 의미](/assets/images/2021/06/20210610_07.png "사전적의미")

---
title:  "[애드브릭스] Flutter & Adbrix & Google Analytics"
date:   2021-07-01 08:19:00 +0900
categories: flutter
---

회사의 마케팅팀에서 최근 런칭한 앱에 애드브릭스를 연동해달라는 협조요청이 왔다.

Google Analytics 와 유사한 유료 서비스로 처음에는 애드브릭스만으로 끝내려고했지만...

기획파트에서는 또 Google Analytics 가 필요하단다...

그래서 작업하는 김에 둘다 작업하고 결과를 공유한다.

## 애드브릭스

[애드비릭스 소개](https://help.dfinery.io/hc/ko/articles/360007869893-adbrix-%EC%95%A0%EB%93%9C%EB%B8%8C%EB%A6%AD%EC%8A%A4-%EA%B7%B8%EB%A1%9C%EC%8A%A4-%EB%A7%88%EC%BC%80%ED%84%B0%EB%A5%BC-%EC%9C%84%ED%95%9C-%EC%95%B1-%EC%84%B1%EA%B3%BC%EC%B8%A1%EC%A0%95-%EC%86%94%EB%A3%A8%EC%85%98)

사실 유료서비스라 그런지 문서는 잘되어 있어서 어렵지않게 연동 가능하였다.

[애드브릭스 연동 가이드](https://help.dfinery.io/hc/ko/articles/900000507886-%EC%95%A0%EB%93%9C%EB%B8%8C%EB%A6%AD%EC%8A%A4-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-Flutter-)

## Google Analytics

이미 Firebase Message 를 사용하고 있기 때문에 별도의 추가 구성없이 `firebase_analytics` 라이브러리를 사용하여 간단하게 연동이 가능하였다.

[pub.dev 페이지](https://pub.dev/packages/firebase_analytics)

각 메뉴이동은 Flutter 의 `navigatorObservers` 에 등록하여 간단하게 처리가 가능하였다.

`firebase_analytics` 는 Observer를 기본으로 제공하지만 애드브릭스는 제공하지 않으며, 각 화면을 기록하는 전송 메소드도 없다.(내가 모르는건가?)

그래서 애드브릭스는 직접 Observer를 작성하고 커스텀이벤트 전송 기능을 활용하여 각 화면의 내역을 전송하였다.

#### 옵저버설정
```dart
FirebaseAnalytics analytics = FirebaseAnalytics();
GetMaterialApp(
  home: Splash(),
  theme: themeData,
  navigatorObservers: [
    FirebaseAnalyticsObserver(analytics: analytics),
    AdBrixObserver(),
  ],
  ... 중략
```

#### AdBrixObserver
```dart
class AdBrixObserver extends RouteObserver<PageRoute<dynamic>> {
  String defaultNameExtractor(RouteSettings settings) => settings.name;

  void _sendScreenView(PageRoute<dynamic> route) {
    final screenName = defaultNameExtractor(route.settings);
    if (screenName != null) {
      AnalyticsCollector().sendCustomEvent(screenName);
    }
  }

  @override
  void didPush(Route<dynamic> route, Route<dynamic> previousRoute) {
    super.didPush(route, previousRoute);
    if (route is PageRoute) {
      _sendScreenView(route);
    }
  }

  @override
  void didReplace({Route<dynamic> newRoute, Route<dynamic> oldRoute}) {
    super.didReplace(newRoute: newRoute, oldRoute: oldRoute);
    if (newRoute is PageRoute) {
      _sendScreenView(newRoute);
    }
  }

  @override
  void didPop(Route<dynamic> route, Route<dynamic> previousRoute) {
    super.didPop(route, previousRoute);
    if (previousRoute is PageRoute && route is PageRoute) {
      _sendScreenView(previousRoute);
    }
  }
}
```
#### 메뉴이동을 제외한 고유한 이벤트 처리를 위한 AnalyticsCollector
회사 비밀이므로 로그인만 공개한다..
```dart

class AnalyticsCollector {
  final dd = DateFormat('yyyy-MM-dd');
  final getIdfa = false;
  static final AnalyticsCollector _instance = AnalyticsCollector._internal();

  factory AnalyticsCollector() {
    return _instance;
  }

  AnalyticsCollector._internal() {
    AdBrixRm.sdkInit(appKey: '너의 앱키', secretKey: '비밀키', delayTime: 3);
    if (getIdfa == true) {
      AdBrixRm.startGettingIDFA();
    } else {
      AdBrixRm.stopGettingIDFA();
    }
    AdBrixRm.setLogLevel(logLevel: AdBrixLogLevel.INFO);
    AdBrixRm.setEventUploadCountInterval(interval: AdBrixEventUploadCountInterval.MIN);
    AdBrixRm.setEventUploadTimeInterval(interval: AdBrixEventUploadTimeInterval.MIN);
  }

  void login(String userId) async {
    await FBMessage().analytics.setUserId(userId);
    await FBMessage().analytics.logLogin(loginMethod: '로그인방법');
    AdBrixRm.login(userId: userId);
  }

  void logout() {
    AdBrixRm.logout();
  }

  /// 회원가입
  void signUp() async {
    var attr = await _getProperties();
    await FBMessage().analytics.logSignUp(signUpMethod: '가입방법');
    AdBrixRm.commonSignUp(channel: AdBrixSignUpChannel.Naver, attr: attr);
  }

  void sendCustomEvent(String eventName) async {
    var attr = await _getProperties();
    AdBrixRm.events(eventName: eventName, attr: attr);
  }

  Future<Map<String, dynamic>> _getProperties() async {
    final format = DateFormat('yyyy-MM-dd');
    var attr = <String, dynamic>{
      'date': format.format(DateTime.now()),
      'channel': 1,
      'platform': GetPlatform.isAndroid ? 'AOS' : 'IOS',
    };
    return attr;
  }
}
```

####애드브릭스 데이터 확인

모든 작업을 마쳤다면 애드브릭스는 사이트에서 제공하는 [콘솔](https://console.dfinery.io/select-account) 에서 바로 실시간 전송되는 모습을 확인 가능하다.

####Google Analytics 데이터 확인

Google Analytics 는 시간이 오래걸리므로 바로 확인하려면 [콘솔](http://console.firebase.google.com)에서 제공하는 디버그 화면에서 확인해야 한다.

아래 명령을 실행하고...
````shell
adb shell setprop debug.firebase.analytics.app 앱패키지명
````

콘솔 > 애널리틱스 > DebugView

![콘솔화면](/assets/images/2021/07/20210701_01.png)


---
title:  "Flutter Firebase Message Custom Sound"
date:   2021-06-18 17:04:00 +0900
categories: flutter
---

앱개발을 잘모르는 나에게 시련이 닥쳤으니 앱의 푸시 알림에 커스텀 사운드를 설정하고 클릭시 각 화면으로 이동하는 것을 구현하는 임무를 받았다.

해본적 없는 것이지만 자신있게 덤볐지만 기존에 만들다만 소스가 날 더욱 혼란스럽게 만들어 반나절 정도 삽질 한 것 같다.

아래 구현 핵심만 설명한다.

##FCM 전송 파라미터 설정

안드로이드 / 아이폰 모두 전송하는 Json 파라미터에서 사운드를 설정할 수 있다.

```json
{
  "to": "너의토큰",
  "notification": {
    "title":"제목",
    "body":"내용",
    "sound":"아이폰/안드로이드 실행파일명(확장자까지)",
    "android_channel_id":"알림채널"
  }
}
```

###Android sound 위치
  /res/raw/[파일명].mp3

###IOS sound 위치
  /[파일명].aiff

프로젝트에 에셋으로 추가해야 한다.

위에 것들을 모두 마쳤다면

#### onSelectNotification 실행중 알람을 눌렀을때 처리
```dart
final initializationSettingsAndroid = AndroidInitializationSettings('@mipmap/ic_launcher');
final initializationSettingsIOS = IOSInitializationSettings();
final initializationSettings = InitializationSettings(android: initializationSettingsAndroid, iOS: initializationSettingsIOS);

await flutterLocalNotificationsPlugin.initialize(initializationSettings, onSelectNotification: onSelectNotification);
```

#### Foreground 알람이 왔을 때
앱이 실행중이면 알람이 오지 않으므로 여기에 리스너를 달아서 강제 알람처리
```dart
FirebaseMessaging.onMessage.listen(_firebaseMessagingBackgroundHandler);
```

#### 앱이 실행되지 않은 상태에서 알람을 눌렀을 때 처리
최초 앱이 실행될때 메시지를 받아서 화면 분기 처리
```dart
_message = await FirebaseMessaging.instance.getInitialMessage();
```

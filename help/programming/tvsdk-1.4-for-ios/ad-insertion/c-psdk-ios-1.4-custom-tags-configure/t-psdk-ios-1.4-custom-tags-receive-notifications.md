---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 알림 수신기를 구현합니다.
title: 시간 초과된 메타데이터 알림에 대한 리스너 추가
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 시간 초과된 메타데이터 알림에 대한 리스너 추가 {#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 알림 수신기를 구현합니다.

관련 활동을 애플리케이션에 알리는 다음 이벤트를 수신하여 시간 메타데이터를 모니터링할 수 있습니다.

* `PTTimedMetadataChangedNotification`: 콘텐츠를 구문 분석하는 동안 고유한 구독 태그가 식별될 때마다 TVSDK는 새 태그를 준비합니다 `PTTimedMetadata` 이 알림에 액세스하고 알림을 전달합니다.

  개체에는 구독한 태그의 이름, 이 태그가 표시되는 재생 내 현지 시간 및 기타 데이터가 포함되어 있습니다.

* `PTMediaPlayerTimeChangeNotification` : 매니페스트/재생 목록이 주기적으로 새로 고치는 라이브/선형 스트림의 경우 업데이트된 재생 목록/매니페스트에 추가 사용자 지정 태그가 나타날 수 있으므로 추가 `TimedMetadata` 개체가 `MediaPlayerItem.timedMetadata` 속성.

  이 이벤트는 이러한 상황이 발생하면 애플리케이션에 알립니다.

  다음 방법 중 하나로 시간 메타데이터를 검색합니다.

   * 응용 프로그램을 설정하여에 자신을 리스너로 추가합니다. `PTTimedMetadataChangedNotification` 을(를) 사용하여 알림 및 개체 가져오기 `PTTimedMetadataKey`.

     ```
     [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
       name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
     
     - (void) onTimedMetadataChanged:(NSNotification *) notification { 
         NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
         PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
     }
     ```

   * 액세스 `timedMetadataCollection` 다음의 속성 `PTMediaPlayerItem`, 다음 항목으로 구성됩니다. `PTTimedMetadata` 지금까지 알림을 받은 오브젝트.

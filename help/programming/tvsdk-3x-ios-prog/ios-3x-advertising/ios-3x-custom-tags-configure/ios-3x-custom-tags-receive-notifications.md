---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 알림 수신기를 구현합니다.
seo-description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 알림 수신기를 구현합니다.
seo-title: 시간 메타데이터 알림에 대한 리스너 추가
title: 시간 메타데이터 알림에 대한 리스너 추가
uuid: b6939011-a6ff-4342-8e7c-3a0c805ee91c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 시간 메타데이터 알림에 대한 리스너 추가 {#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 알림 수신기를 구현합니다.

애플리케이션에 관련 활동을 알리는 다음 이벤트를 수신하여 시간 지정 메타데이터를 모니터링할 수 있습니다.

* `PTTimedMetadataChangedNotification`:콘텐츠를 구문 분석하는 동안 고유 구독 태그가 식별될 때마다 TVSDK는 새 `PTTimedMetadata` 개체를 준비하고 이 알림을 전달합니다.

   개체에는 구독한 태그의 이름, 이 태그가 나타날 재생 중인 로컬 시간 및 기타 데이터가 포함됩니다.

* `PTMediaPlayerTimeChangeNotification` :매니페스트/재생 목록이 정기적으로 새로 고쳐지는 라이브/선형 스트림의 경우 업데이트된 재생 목록/매니페스트에 추가 사용자 지정 태그가 나타날 수 있으므로 추가 `TimedMetadata` 개체가 `MediaPlayerItem.timedMetadata` 속성에 추가될 수 있습니다.

   이 이벤트는 이러한 경우 응용 프로그램에 알립니다.

   다음 방법 중 하나로 시간 메타데이터를 검색합니다.

   * 응용 프로그램을 설정하여 `PTTimedMetadataChangedNotification` 알림에 리스너로 추가하고 을 사용하여 객체를 페치합니다 `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * 지금까지 알림을 받은 모든 `timedMetadataCollection` 개체로 구성된 `PTMediaPlayerItem``PTTimedMetadata` 속성 액세스
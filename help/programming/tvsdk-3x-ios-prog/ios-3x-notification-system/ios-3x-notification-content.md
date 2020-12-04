---
description: PTNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류도 플레이어의 상태가 변경됩니다.
seo-description: PTNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류도 플레이어의 상태가 변경됩니다.
seo-title: 알림 컨텐츠
title: 알림 컨텐츠
uuid: d42d2e89-1bdd-4be0-8a69-821fec6bbc75
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# 플레이어 상태, 활동, 오류 및 로깅에 대한 알림 {#notifications-player-status-activity-errors-logging}

`PTNotification` 개체는 플레이어 상태, 경고 및 오류의 변경 사항에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류도 플레이어의 상태가 변경됩니다.

응용 프로그램에서 알림 및 상태 정보를 검색할 수 있습니다. 알림 정보를 사용하여 진단 및 유효성 검사를 위한 로깅 시스템을 만들 수도 있습니다.

>[!NOTE]
>
>또한 TVSDK는 플레이어 활동에 대한 정보를 제공하기 위해 전달되는 `NSNotifications`( `PTMediaPlayer` 알림) *`event`* 알림을 참조하기 위해 *`notification`*&#x200B;을 사용합니다.

또한 TVSDK가 `PTNotification`을(를) 발행할 때 `PTMediaPlayerNewNotificationItemEntryNotification`을(를) 발행합니다.

이벤트를 캡처하고 응답하도록 이벤트 리스너를 구현합니다. 많은 이벤트가 `PTNotification` 상태 알림을 제공합니다.

## 알림 내용 {#notification-content}

`PTNotification` 플레이어 상태와 관련된 정보를 제공합니다.

TVSDK는 `PTNotification` 알림의 시간순 목록을 제공합니다. 각 알림은 다음 정보를 포함합니다.

* 타임스탬프
* 다음 요소로 구성된 진단 메타데이터:

   * `type`:정보, 경고 또는 오류입니다.
   * `code`:알림의 숫자 표현입니다.
   * `name`:사용자가 읽을 수 있는 알림 설명(예: SEEK_ERROR)
   * `metadata`:알림에 대한 관련 정보가 들어 있는 키/값 쌍입니다. 예를 들어 `URL`이라는 키는 알림과 관련된 URL인 값을 제공합니다.

   * `innerNotification`:이 알림에 직접 영향을 주는 다른  `PTNotification` 개체에 대한 참조입니다.

나중에 분석을 위해 이 정보를 로컬에 저장하거나 원격 서버에 보내 로깅 및 그래픽 표현을 할 수 있습니다.

## 알림 설정 {#notification-setup}

사용자 지정 알림에 대해 동일한 설정을 완료해야 하지만 TVSDK는 기본 알림에 대해 플레이어를 설정합니다.

`PTNotification`에 대한 두 가지 구현이 있습니다.

* 청각
* 사용자 지정 알림을 `PTNotificationHistory`에 추가하려면

TVSDK는 알림을 듣기 위해 `PTNotification` 클래스를 인스턴스화하여 PTMediaPlayer 인스턴스에 연결된 `PTMediaPlayerItem` 인스턴스에 첨부합니다. `PTMediaPlayer`에 대해 하나의 `PTNotificationHistory` 인스턴스만 있습니다.

>[!IMPORTANT]
>
>TVSDK가 아닌 사용자 정의 설정을 추가하는 경우 해당 단계를 수행해야 합니다.

## 알림 수신{#listen-to-notifications}

`PTMediaPlayer`에서 `PTNotification` 알림을 수신하는 방법에는 두 가지가 있습니다.

1. 타이머와 함께 `PTMediaPlayerItem`의 `PTNotificationHistory`을(를) 수동으로 확인하고 차이점을 확인합니다.

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`의 게시된 [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html)을 사용하십시오.
1. 알림을 받을 `PTMediaPlayer`의 인스턴스를 사용하여 `NSNotification`에 등록합니다.

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 알림 콜백 구현 {#implement-notification-callbacks}

알림 콜백을 구현할 수 있습니다.

`NSNotification` 사용자 정보에서 `PTNotification`을(를) 가져오고 `PTMediaPlayerNotificationKey`를 사용하여 해당 값을 읽고 알림 콜백을 구현합니다.

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## 사용자 지정 알림 추가 {#add-custom-notifications}

사용자 지정 알림을 추가하려면:
새 `PTNotification`을(를) 만들고 현재 `PTMediaPlayerItem`를 사용하여 `PTNotificationHistory`에 추가합니다.

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```

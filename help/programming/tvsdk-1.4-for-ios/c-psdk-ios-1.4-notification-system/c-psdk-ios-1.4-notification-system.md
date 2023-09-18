---
description: PTNotification 객체는 플레이어 상태, 경고 및 오류의 변경 내용에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태에도 변화를 일으킵니다.
title: 플레이어 상태, 활동, 오류 및 로그에 대한 알림
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 플레이어 상태, 활동, 오류 및 로깅에 대한 알림  {#notifications-for-player-status-activity-errors-and-logs-overview}

PTNotification 객체는 플레이어 상태, 경고 및 오류의 변경 내용에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태에도 변화를 일으킵니다.

애플리케이션은 알림 및 상태 정보를 검색할 수 있습니다. 알림 정보를 사용하여 진단 및 유효성 검사를 위한 로깅 시스템을 만들 수도 있습니다.

>[!IMPORTANT]
>
>TVSDK는 *`notification`* 을(를) 참조하려면 `NSNotifications` ( `PTMediaPlayer` 알림) *`event`* 플레이어 활동에 대한 정보를 제공하기 위해 발송되는 알림입니다.

TVSDK도 문제 `PTMediaPlayerNewNotificationItemEntryNotification` 문제 발생 시 `PTNotification`.

이벤트 리스너를 구현하여 이벤트를 캡처하고 응답합니다. 많은 이벤트가 다음을 제공합니다 `PTNotification` 상태 알림입니다.

## 알림 콘텐츠 {#notification-content}

PTNotification 은 플레이어의 상태와 관련된 정보를 제공합니다.

TVSDK는 의 시간 순 목록을 제공합니다. `PTNotification` 알림입니다. 각 알림에는 다음 정보가 포함됩니다.

* 타임스탬프
* 다음 요소로 구성된 진단 메타데이터:

   * `type`: 정보, 경고 또는 오류.
   * `code`: 알림의 숫자 표현입니다.
   * `name`: 사람이 인식할 수 있는 알림 설명(예: SEEK_ERROR)
   * `metadata`: 알림에 대한 관련 정보가 포함된 키/값 쌍. 예를 들어 `URL` 알림과 관련된 URL인 값을 제공합니다.

   * `innerNotification`: 다른 참조에 대한 참조 `PTNotification` 이 알림에 직접 영향을 주는 개체입니다.

나중에 분석할 수 있도록 이 정보를 로컬에 저장하거나 로깅 및 그래픽 표시를 위해 원격 서버로 전송할 수 있습니다.

## 알림 설정 {#notification-setup}

사용자 지정 알림에 대해 동일한 설정을 완료해야 하지만, TVSDK는 기본 알림에 대해 플레이어를 설정합니다.

에는 두 가지 구현이 있습니다 `PTNotification`:

* 듣다
* 에 사용자 지정 알림을 추가하려면 `PTNotificationHistory`

알림을 수신하기 위해 TVSDK는 `PTNotification` 클래스를 만들고 이 클래스를 의 인스턴스에 연결합니다. `PTMediaPlayerItem`: PTMediaPlayer 인스턴스에 첨부됩니다. 하나만 있습니다. `PTNotificationHistory` 인스턴스 `PTMediaPlayer`.

>[!IMPORTANT]
>
>사용자 지정을 추가하는 경우 TVSDK가 아닌 애플리케이션이 해당 단계를 수행해야 합니다.

## 알림 수신 {#listen-to-notifications}

다음 두 가지 방법으로 음악을 들을 수 있습니다. `PTNotification` 의 알림 `PTMediaPlayer`:

1. 수동으로 확인 `PTNotificationHistory` / `PTMediaPlayerItem` 타이머를 사용하여 차이점 확인:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 게시한 항목 사용 [NSN 알림](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) / `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. 에 등록 `NSNotification` 의 인스턴스를 사용하여 `PTMediaPlayer` 알림을 받을 원본:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 알림 콜백 구현 {#implement-notification-callbacks}

알림 콜백을 구현할 수 있습니다.

1. 다음을 가져와 알림 콜백 구현 `PTNotification` 다음에서 `NSNotification` 사용자 정보 및 를 사용하여 해당 값 읽기 `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## 사용자 지정 알림 추가 {#add-custom-notifications}

사용자 지정 알림을 추가하려면: 새로 만들기 `PTNotification` 및에 추가합니다. `PTNotificationHistory` 현재 사용 `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```

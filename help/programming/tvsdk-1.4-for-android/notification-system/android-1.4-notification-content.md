---
description: MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류도 플레이어의 상태가 변경됩니다.
seo-description: MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류도 플레이어의 상태가 변경됩니다.
seo-title: 알림 컨텐츠
title: 알림 컨텐츠
uuid: 89fb8f63-b0d5-45cd-bdad-348529fd07d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# 알림 내용 {#notification-content}

MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류도 플레이어의 상태가 변경됩니다.

응용 프로그램에서 알림 및 상태 정보를 검색할 수 있습니다. 알림 정보를 사용하여 진단 및 유효성 검사를 위한 로깅 시스템을 만들 수도 있습니다.

이벤트를 캡처하고 응답하도록 이벤트 리스너를 구현합니다. 많은 이벤트가 `MediaPlayerNotification` 상태 알림을 제공합니다.

`MediaPlayerNotification` 플레이어 상태와 관련된 정보를 제공합니다.

TVSDK는 `MediaPlayerNotification` 알림의 시간순 목록을 제공합니다. 각 알림은 다음 정보를 포함합니다.

* 타임스탬프
* 다음 요소로 구성된 진단 메타데이터:

   * `type`:정보, 경고 또는 오류입니다.
   * `code`:알림의 숫자 표현입니다.
   * `name`:사용자가 읽을 수 있는 알림 설명(예: SEEK_ERROR)
   * `metadata`:알림에 대한 관련 정보가 들어 있는 키/값 쌍입니다. 예를 들어 `URL`이라는 키는 알림과 관련된 URL인 값을 제공합니다.

   * `innerNotification`:이 알림에 직접 영향을 주는 다른  `MediaPlayerNotification` 개체에 대한 참조입니다.

나중에 분석을 위해 이 정보를 로컬에 저장하거나 원격 서버에 보내 로깅 및 그래픽 표현을 할 수 있습니다.

## 알림 시스템 {#set-up-your-notification-system} 설정

알림을 수신하고 자신만의 알림을 알림 내역에 추가할 수 있습니다.

Primetime 플레이어 알림 시스템의 핵심은 독립형 알림을 나타내는 `Notification` 클래스입니다.

`NotificationHistory` 클래스는 알림을 축적하는 메커니즘을 제공합니다. 알림 컬렉션을 나타내는 알림 로그(NotificationHistoryItem) 개체를 저장합니다.

알림을 수신하려면:

* 알림 수신
* 알림 기록에 알림 추가

1. 상태 변화에 귀를 기울입니다.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` 콜백을 구현합니다.
1. TVSDK는 콜백으로 두 개의 매개 변수를 전달합니다.

   * 새 상태( `MediaPlayer.PlayerState`)
   * `MediaPlayerNotification` 개체

## 실시간 로깅 및 디버깅 추가 {#add-real-time-logging-and-debugging}

알림을 사용하여 비디오 애플리케이션에서 실시간 로깅을 구현할 수 있습니다.

알림 시스템을 사용하면 시스템을 과도하게 강조하지 않고도 진단 및 유효성 검사를 위한 로깅 및 디버깅 정보를 수집할 수 있습니다.

>[!IMPORTANT]
>
>로깅 백 엔드는 프로덕션 설정의 일부가 아니며 고로드 트래픽을 처리하지 못할 것입니다. 구현을 완전히 완료할 필요가 없는 경우 시스템 과부하 방지를 위해 데이터 전송 효율성을 고려하십시오.

다음은 알림을 검색하는 방법의 예입니다.

1. TVSDK 알림 시스템에서 수집한 데이터를 정기적으로 쿼리하는 비디오 응용 프로그램에 대한 타이머 기반 실행 스레드를 만듭니다.

1. 타이머의 간격이 너무 크고 이벤트 목록의 크기가 너무 작으면 알림 이벤트 목록이 오버플로됩니다. 이 오버플로우를 방지하려면 다음 중 하나를 수행하십시오.

   * 새 이벤트를 폴링하는 스레드를 유도하는 시간 간격을 줄입니다.
   * 알림 목록의 크기를 늘립니다.

1. JSON 형식의 최신 알림 이벤트 항목을 일련화하고 후처리를 위해 원격 서버에 항목을 보냅니다.

   그러면 원격 서버가 제공된 데이터를 실시간으로 그래픽으로 표시할 수 있습니다.
1. 알림 이벤트의 손실을 검색하려면 이벤트 인덱스 값 시퀀스에서 간격을 찾습니다.

   각 알림 이벤트에는 `session.NotificationHistory` 클래스에 의해 자동으로 증가되는 인덱스 값이 있습니다.

## ID3 태그 {#id-tags}

ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.

>[!IMPORTANT]
>
>TVSDK는 가능한 인코딩(ASCII, UTF8, UTF16-BE 또는 UTF16-LE)에서 오디오(AAC) 및 비디오(H.264) 스트림의 ID3 메타데이터(버전 2.3.0 또는 2.4.0)를 인식합니다. 인식된 버전 또는 형식 중 하나에 포함되지 않은 ID3 태그를 무시합니다. 지정되지 않은 인코딩은 UTF8로 처리됩니다.

TVSDK에서 ID3 메타데이터를 감지하면 다음 데이터가 포함된 알림을 발행합니다.

* InfoCode = 303007
* TYPE = ID3
* NAME = 없음
* ID = 0

1. `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)`에 대한 이벤트 리스너를 구현하고 `MediaPlayer` 개체에 등록합니다.

   TVSDK는 ID3 메타데이터를 감지하면 이 수신기를 호출합니다.

   >[!NOTE]
   >
   >사용자 지정 광고 큐는 동일한 `onTimedMetadata` 이벤트를 사용하여 새 태그 탐지를 나타냅니다. 이로 인해 매니페스트 수준에서 사용자 지정 광고 큐가 검색되고 ID3 태그가 스트림에 포함되기 때문에 혼란이 발생해서는 안됩니다. 자세한 내용은 사용자 지정 태그 구성을 참조하십시오.

1. 메타데이터를 검색합니다.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```

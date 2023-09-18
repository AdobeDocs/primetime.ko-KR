---
description: MediaPlayerNotification 개체는 플레이어 상태 변경, 경고 및 오류에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태에도 변화를 일으킵니다.
title: 알림 콘텐츠
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 알림 콘텐츠 {#notification-content}

MediaPlayerNotification 개체는 플레이어 상태 변경, 경고 및 오류에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태에도 변화를 일으킵니다.

애플리케이션은 알림 및 상태 정보를 검색할 수 있습니다. 알림 정보를 사용하여 진단 및 유효성 검사를 위한 로깅 시스템을 만들 수도 있습니다.

이벤트 리스너를 구현하여 이벤트를 캡처하고 응답합니다. 많은 이벤트가 다음을 제공합니다 `MediaPlayerNotification` 상태 알림입니다.

`MediaPlayerNotification` 는 플레이어 상태와 관련된 정보를 제공합니다.

TVSDK는 의 시간 순 목록을 제공합니다. `MediaPlayerNotification` 알림입니다. 각 알림에는 다음 정보가 포함됩니다.

* 타임스탬프
* 다음 요소로 구성된 진단 메타데이터:

   * `type`: 정보, 경고 또는 오류.
   * `code`: 알림의 숫자 표현입니다.
   * `name`: 사람이 인식할 수 있는 알림 설명(예: SEEK_ERROR)
   * `metadata`: 알림에 대한 관련 정보가 포함된 키/값 쌍. 예를 들어 `URL` 알림과 관련된 URL인 값을 제공합니다.

   * `innerNotification`: 다른 참조에 대한 참조 `MediaPlayerNotification` 이 알림에 직접 영향을 주는 개체입니다.

나중에 분석할 수 있도록 이 정보를 로컬에 저장하거나 로깅 및 그래픽 표시를 위해 원격 서버로 전송할 수 있습니다.

## 알림 시스템 설정 {#set-up-your-notification-system}

알림을 수신하고 고유한 알림을 알림 기록에 추가할 수 있습니다.

Primetime 플레이어 알림 시스템의 핵심은 입니다. `Notification` 클래스: 독립 실행형 알림을 나타냅니다.

다음 `NotificationHistory` 클래스는 알림을 누적하는 메커니즘을 제공합니다. 알림의 컬렉션을 나타내는 알림 로그(NotificationHistoryItem) 개체를 저장합니다.

알림을 받으려면:

* 알림 수신
* 알림 기록에 알림 추가

1. 상태 변경 내용을 수신합니다.
1. 구현 `MediaPlayer.PlaybackEventListener.onStateChanged` callback.
1. TVSDK는 두 개의 매개 변수를 콜백에 전달합니다.

   * 새 상태( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 오브젝트

## 실시간 로깅 및 디버깅 추가 {#add-real-time-logging-and-debugging}

알림을 사용하여 비디오 애플리케이션에서 실시간 로깅을 구현할 수 있습니다.

알림 시스템을 사용하면 시스템에 과도한 부담을 주지 않고도 진단 및 유효성 검사를 위한 로깅 및 디버깅 정보를 수집할 수 있습니다.

>[!IMPORTANT]
>
>로깅 백 엔드는 프로덕션 설정의 일부가 아니므로 높은 로드 트래픽을 처리할 수 없습니다. 구현이 절대적으로 완료되지 않아도 되는 경우 데이터 전송의 효율성을 고려하여 시스템을 오버로드할 수 있습니다.

다음은 알림을 검색하는 방법의 예입니다.

1. TVSDK 알림 시스템에서 수집한 데이터를 정기적으로 쿼리하는 비디오 응용 프로그램에 대한 타이머 기반 실행 스레드를 만듭니다.

1. 타이머의 간격이 너무 크고 이벤트 목록의 크기가 너무 작으면 알림 이벤트 목록이 오버플로됩니다. 이 오버플로를 방지하려면 다음 중 하나를 수행합니다.

   * 새 이벤트에 대해 폴링하는 스레드를 구동하는 시간 간격을 줄입니다.
   * 알림 목록의 크기를 늘립니다.

1. 최신 알림 이벤트 항목을 JSON 형식으로 serialize하고 사후 처리를 위해 원격 서버로 해당 항목을 보냅니다.

   그런 다음 원격 서버는 제공된 데이터를 실시간으로 그래픽으로 표시할 수 있다.
1. 알림 이벤트의 손실을 탐지하려면 이벤트 색인 값의 순서에서 간격을 찾습니다.

   각 알림 이벤트에는 `session.NotificationHistory` 클래스.

## ID3 태그 {#id-tags}

ID3 태그는 파일 제목 또는 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션은 태그로부터 데이터를 추출할 수 있습니다.

>[!IMPORTANT]
>
>TVSDK는 오디오(AAC) 및 비디오(H.264) 스트림에서 가능한 인코딩(ASCII, UTF8, UTF16-BE 또는 UTF16-LE)으로 ID3 메타데이터(버전 2.3.0 또는 2.4.0)를 인식합니다. 인식된 버전 또는 형식 중 하나에 없는 ID3 태그는 무시됩니다. 지정되지 않은 인코딩은 UTF8로 처리됩니다.

TVSDK가 ID3 메타데이터를 감지하면 다음 데이터로 알림을 보냅니다.

* InfoCode = 303007
* 유형 = ID3
* 이름 = 없음
* ID = 0

1. 에 대한 이벤트 리스너 구현 `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 다음을 통해 등록: `MediaPlayer` 개체.

   TVSDK는 ID3 메타데이터를 감지하면 이 리스너를 호출합니다.

   >[!NOTE]
   >
   >사용자 정의 광고 큐는 동일한 `onTimedMetadata` 새 태그의 감지를 나타내는 이벤트입니다. 사용자 지정 광고 큐가 매니페스트 수준에서 검색되고 ID3 태그가 스트림에 포함되므로 혼동을 일으키지 않아야 합니다. 자세한 내용은 사용자 지정 태그 구성 을 참조하십시오.

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

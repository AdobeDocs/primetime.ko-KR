---
description: MediaPlayerItem.timedMetadata 속성을 사용하면 재생 목록/매니페스트 태그 또는 미디어 스트림 내의 ID3 태그에서 만든 모든 TimedMetadata 개체에 액세스할 수 있습니다. MediaPlayerItem.hasTimedMetadata 속성은 구독한 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다.
title: 매니페스트 태그에 대한 알림
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 매니페스트 태그에 대한 알림{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata 속성을 사용하면 재생 목록/매니페스트 태그 또는 미디어 스트림 내의 ID3 태그에서 만든 모든 TimedMetadata 개체에 액세스할 수 있습니다. MediaPlayerItem.hasTimedMetadata 속성은 구독한 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다.

관련 활동을 애플리케이션에 알리는 다음 이벤트를 수신하여 시간 메타데이터를 모니터링할 수 있습니다.

* `MediaPlayerItemEvent.ITEM_CREATED`: 의 초기 목록 `TimedMetadata` 객체는 다음 이후에서 사용할 수 있습니다. `MediaPlayerItem` 이(가) 만들어졌습니다. 이 이벤트는 이러한 상황이 발생하면 애플리케이션에 알립니다.

* `MediaPlayerItemEvent.ITEM_UPDATED`: 매니페스트/재생 목록이 주기적으로 새로 고치는 라이브/선형 스트림의 경우 업데이트된 재생 목록/매니페스트에 추가 사용자 지정 태그가 나타날 수 있으므로 TimedMetadata 개체를 `MediaPlayerItem.timedMetadata` 속성. 이 이벤트는 이러한 상황이 발생하면 애플리케이션에 알립니다.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: 매번 새로 `TimedMetadata` 개체가 생성되면 이 이벤트는에 의해 전달됩니다. `MediaPlayer`. 이 이벤트는 다음에 대해 발송되지 않습니다. `TimedMetadata` 초기화 단계에서 생성된 객체입니다.

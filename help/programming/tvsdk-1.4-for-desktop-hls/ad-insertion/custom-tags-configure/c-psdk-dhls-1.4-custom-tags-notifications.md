---
description: MediaPlayerItem.timedMetadata 속성을 사용하면 재생 목록/매니페스트 태그 또는 미디어 스트림 내의 ID3 태그에서 만든 모든 TimedMetadata 개체에 액세스할 수 있습니다. MediaPlayerItem.hasTimedMetadata 속성은 구독된 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다.
seo-description: MediaPlayerItem.timedMetadata 속성을 사용하면 재생 목록/매니페스트 태그 또는 미디어 스트림 내의 ID3 태그에서 만든 모든 TimedMetadata 개체에 액세스할 수 있습니다. MediaPlayerItem.hasTimedMetadata 속성은 구독된 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다.
seo-title: 매니페스트 태그에 대한 알림
title: 매니페스트 태그에 대한 알림
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# 매니페스트 태그에 대한 알림{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata 속성을 사용하면 재생 목록/매니페스트 태그 또는 미디어 스트림 내의 ID3 태그에서 만든 모든 TimedMetadata 개체에 액세스할 수 있습니다. MediaPlayerItem.hasTimedMetadata 속성은 구독된 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다.

애플리케이션에 관련 활동을 알리는 다음 이벤트를 수신하여 시간 메타데이터를 모니터링할 수 있습니다.

* `MediaPlayerItemEvent.ITEM_CREATED`:개체의 초기 목록을 만든 후  `TimedMetadata` 사용할 수  `MediaPlayerItem` 있습니다. 이 이벤트는 이러한 경우 응용 프로그램에 알립니다.

* `MediaPlayerItemEvent.ITEM_UPDATED`:매니페스트/재생 목록이 정기적으로 새로 고쳐지는 라이브/선형 스트림의 경우 업데이트된 재생 목록/매니페스트에 추가 사용자 지정 태그가 나타날 수 있으므로 추가 TimedMetadata 개체를  `MediaPlayerItem.timedMetadata` 속성에 추가할 수 있습니다. 이 이벤트는 이러한 경우 응용 프로그램에 알립니다.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:새  `TimedMetadata`   `MediaPlayer`개체를 만들 때마다 이 이벤트는 이 이벤트는 초기화 단계 동안 만들어진 `TimedMetadata` 개체에 대해 전달되지 않습니다.


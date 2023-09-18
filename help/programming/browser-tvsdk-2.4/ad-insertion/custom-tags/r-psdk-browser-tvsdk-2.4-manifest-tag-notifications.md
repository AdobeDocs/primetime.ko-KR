---
description: MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그 또는 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.
title: 매니페스트 태그에 대한 알림
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 매니페스트 태그에 대한 알림{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그 또는 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

다음 `MediaPlayerItem.hasTimedMetadata` 속성은 구독한 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다. 을(를) 수신하여 시간 메타데이터를 모니터링할 수 있습니다. `Events.TimedMetadataEvent`: 매번 새로 만들 때마다 MediaPlayer 인스턴스가 디스패치합니다. `TimedMetadata` 개체가 만들어집니다.

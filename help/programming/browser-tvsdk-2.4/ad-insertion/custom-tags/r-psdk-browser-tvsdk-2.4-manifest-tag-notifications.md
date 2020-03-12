---
description: MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그나 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.
seo-description: MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그나 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.
seo-title: 매니페스트 태그에 대한 알림
title: 매니페스트 태그에 대한 알림
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 매니페스트 태그에 대한 알림{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그나 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

이 `MediaPlayerItem.hasTimedMetadata` 속성은 구독된 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다. 새 `Events.TimedMetadataEvent``TimedMetadata` 개체가 생성될 때마다 MediaPlayer 인스턴스가 전달하는 시간 메타데이터를 수신하여 모니터링할 수 있습니다.

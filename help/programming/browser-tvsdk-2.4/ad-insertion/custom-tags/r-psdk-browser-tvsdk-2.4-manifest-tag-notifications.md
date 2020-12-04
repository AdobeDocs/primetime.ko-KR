---
description: MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그 또는 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.
seo-description: MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그 또는 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.
seo-title: 매니페스트 태그에 대한 알림
title: 매니페스트 태그에 대한 알림
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 매니페스트 태그에 대한 알림{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata 속성은 재생 목록/매니페스트 태그 또는 미디어 스트림의 ID3 태그에서 만든 모든 TimedMetadata 개체에 대한 액세스를 제공합니다.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

`MediaPlayerItem.hasTimedMetadata` 속성은 구독된 사용자 지정 태그가 현재 미디어에 있는지 여부를 나타냅니다. MediaPlayer 인스턴스가 새 `TimedMetadata` 개체를 만들 때마다 전달하는 `Events.TimedMetadataEvent`에 대한 의견을 수렴하여 시간 메타데이터를 모니터링할 수 있습니다.

---
description: TVSDK는 시간 메타데이터 작업에 대한 응답으로 광고 제공 이벤트를 전달합니다.
seo-description: TVSDK는 시간 메타데이터 작업에 대한 응답으로 광고 제공 이벤트를 전달합니다.
seo-title: 광고 서비스/시간 메타데이터 이벤트
title: 광고 서비스/시간 메타데이터 이벤트
uuid: fd50a937-0c9b-4c47-acb2-1ffc0592ad54
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 광고 제공/시간 메타데이터 이벤트{#ad-serving-timed-metadata-events}

TVSDK는 시간 메타데이터 작업에 대한 응답으로 광고 제공 이벤트를 전달합니다.

이러한 모든 관련 이벤트에 대한 알림을 받으려면 다음 이벤트에 대해 `MediaPlayer` 개체에 이벤트 리스너를 등록합니다.

| 이벤트 | 의미 |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | ID3 시간 지정 메타데이터가 처리되었습니다. |
| TimedMetadataEvent.[TIMED_METADATA_SKULLED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 시간 지정 메타데이터가 처리되었으며 기회가 검색되지 않았습니다. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 시간 지정 메타데이터를 사용할 수 있으며 기회를 찾을 수 없습니다. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 시간 지정 메타데이터가 처리되었으며 백그라운드 매니페스트에서 기회가 검색되지 않았습니다. |
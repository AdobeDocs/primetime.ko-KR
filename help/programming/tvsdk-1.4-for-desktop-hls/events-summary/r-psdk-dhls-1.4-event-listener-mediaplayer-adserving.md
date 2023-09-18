---
description: TVSDK는 시간 초과된 메타데이터 작업에 대한 응답으로 광고 서비스 제공 이벤트를 전달합니다.
title: 광고 서비스 제공/시간 메타데이터 이벤트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 광고 서비스 제공/시간 메타데이터 이벤트{#ad-serving-timed-metadata-events}

TVSDK는 시간 초과된 메타데이터 작업에 대한 응답으로 광고 서비스 제공 이벤트를 전달합니다.

이러한 모든 관련 이벤트에 대한 알림을 받으려면 이벤트 리스너를 `MediaPlayer` 개체.

| 이벤트 | 의미 |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | ID3 시간 설정 메타데이터를 처리했습니다. |
| TimedMetadataEvent.[TIMED_METADATA_건너뜀](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 시간이 지정된 메타데이터가 처리되었으며 기회가 검색되지 않았습니다. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 시간 메타데이터를 사용할 수 있으며 기회가 검색되지 않았습니다. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 시간 메타데이터가 처리되었으며 백그라운드 매니페스트에서 기회가 검색되지 않았습니다. |

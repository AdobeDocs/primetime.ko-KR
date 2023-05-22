---
description: TVSDK는 QoS(서비스 품질) 이벤트를 전달하여 버퍼링 또는 검색 등 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.
title: QoS 이벤트
exl-id: 7de28d00-12e2-4f2a-bb1b-53661e3578a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# QoS 이벤트{#qos-events}

TVSDK는 QoS(서비스 품질) 이벤트를 전달하여 버퍼링 또는 검색 등 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.

모든 QoS 관련 이벤트에 대한 알림을 받으려면 이벤트 리스너를 `MediaPlayer` 다음 이벤트에 대한 개체:

| 이벤트 | 의미 |
|---|---|
| BufferEvent.[버퍼링 종료](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 버퍼링이 완료되었습니다. |
| BufferEvent.[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 버퍼링이 시작되었습니다. |
| SeekEvent.[찾기 완료됨](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 찾기가 완료되었습니다. |
| SeekEvent.[SEEK_START](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 찾기를 시작하고 있습니다. |
| SeekEvent.[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK가 현재 광고 정책의 결과로 검색 위치를 변경했습니다. |

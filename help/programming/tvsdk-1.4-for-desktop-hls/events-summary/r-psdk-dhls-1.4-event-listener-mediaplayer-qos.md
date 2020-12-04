---
description: TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링이나 검색 등의 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.
seo-description: TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링이나 검색 등의 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.
seo-title: QoS 이벤트
title: QoS 이벤트
uuid: fd657cf0-c6d4-4e9a-b212-7d09d483cae9
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# QoS 이벤트{#qos-events}

TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링이나 검색 등의 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.

모든 QoS 관련 이벤트에 대한 알림을 받으려면 다음 이벤트에 대해 `MediaPlayer` 개체에 이벤트 리스너를 등록합니다.

| 이벤트 | 의미 |
|---|---|
| 버퍼 이벤트.[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 버퍼링이 완료되었습니다. |
| 버퍼 이벤트.[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 버퍼링이 시작되었습니다. |
| SeekEvent.[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 검색 완료 |
| SeekEvent.[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 검색 시작 |
| SeekEvent.[SEEK_POSITION_ADJUTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK는 현 광고 정책의 결과로 검색 위치를 변경했습니다. |


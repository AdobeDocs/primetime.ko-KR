---
description: TVSDK는 미디어 항목 로드에 응답하여 미디어 플레이어 항목 이벤트를 발송합니다.
title: 로더 이벤트
exl-id: ee5be2d4-5c77-4af4-b8fe-8cef18d7c0d9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 로더 이벤트{#loader-events}

TVSDK는 미디어 항목 로드에 응답하여 미디어 플레이어 항목 이벤트를 발송합니다.

이러한 이벤트는 대체 워크플로우를 제공합니다. 를 만들 때 이 인터페이스를 구현할 필요가 없습니다. `MediaPlayer`. 다음 항목을 보유할 때 사용하십시오. `MediaPlayerItemLoader`.

미디어 플레이어 리소스 로드와 관련된 이벤트에 대한 알림을 받으려면 다음에 대한 다음 이벤트에 대한 리스너를 등록하십시오. `MediaPlayerItemLoader` 개체.

| 이벤트 | 의미 |
|---|---|
| MediaPlayerItemLoader.[완료됨](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 미디어 리소스 로드가 완료되었습니다. |
| MediaPlayerItemLoader.[실패](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 미디어 리소스를 로드하는 도중 문제가 발생했습니다. |

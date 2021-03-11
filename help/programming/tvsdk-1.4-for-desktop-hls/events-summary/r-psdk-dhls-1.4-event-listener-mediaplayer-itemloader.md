---
description: TVSDK는 미디어 항목을 로드하는 데 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.
title: 로더 이벤트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 로더 이벤트{#loader-events}

TVSDK는 미디어 항목을 로드하는 데 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.

이러한 이벤트는 대체 워크플로우를 제공합니다. `MediaPlayer`을(를) 만들 때 이 인터페이스를 구현할 필요가 없습니다. `MediaPlayerItemLoader`을(를) 사용하려면 이 옵션을 사용합니다.

미디어 플레이어 리소스 로드와 관련된 이벤트에 대한 알림을 받으려면 `MediaPlayerItemLoader` 객체에 다음 이벤트에 대한 리스너를 등록합니다.

| 이벤트 | 의미 |
|---|---|
| MediaPlayerItemLoader.[완료](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 미디어 리소스 로드가 완료되었습니다. |
| MediaPlayerItemLoader.[실패](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 미디어 리소스를 로드하는 동안 문제가 발생했습니다. |
---
description: TVSDK는 미디어 항목 로딩에 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.
seo-description: TVSDK는 미디어 항목 로딩에 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.
seo-title: 로더 이벤트
title: 로더 이벤트
uuid: 0ad37715-14b1-457c-892f-0db0d6220f0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 로더 이벤트{#loader-events}

TVSDK는 미디어 항목 로딩에 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.

이러한 이벤트는 대체 워크플로우를 제공합니다. You are not required to implement this interface when creating a `MediaPlayer`. 이것을 가지고 싶을 때 `MediaPlayerItemLoader`사용하세요.

미디어 플레이어 리소스 로드와 관련된 이벤트에 대한 알림을 받으려면 `MediaPlayerItemLoader` 개체에 다음 이벤트에 대한 리스너를 등록합니다.

| 이벤트 | 의미 |
|---|---|
| MediaPlayerItemLoader.[완료](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 미디어 리소스 로드가 완료되었습니다. |
| MediaPlayerItemLoader.[실패](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 미디어 리소스를 로드하는 동안 문제가 발생했습니다. |
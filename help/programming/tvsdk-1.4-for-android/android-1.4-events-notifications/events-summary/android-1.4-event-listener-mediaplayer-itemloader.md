---
description: TVSDK는 미디어 항목 로딩에 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.
seo-description: TVSDK는 미디어 항목 로딩에 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.
seo-title: 로더 이벤트
title: 로더 이벤트
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 로더 이벤트{#loader-events}

TVSDK는 미디어 항목 로딩에 대한 응답으로 미디어 플레이어 항목 이벤트를 전달합니다.

이러한 이벤트는 대체 워크플로우를 제공합니다. MediaPlayer를 만들 때는 이 인터페이스를 구현할 필요가 없습니다. 이것을 가지고 싶을 때 `MediaPlayerItemLoader`사용하세요.

미디어 플레이어 리소스 로드와 관련된 이벤트에 대한 알림을 받으려면 다음 이벤트를 `MediaPlayerItemLoader.LoaderListener` 포함하는 구현을 등록합니다.

| 이벤트 | 의미 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 미디어 리소스 로드가 완료되었습니다. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 미디어 리소스를 로드하는 동안 문제가 발생했습니다. |

>[!NOTE]
>
>QoS `onLoadInfo (loadInfo)` 이벤트도 참조하십시오.


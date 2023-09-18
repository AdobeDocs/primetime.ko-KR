---
description: TVSDK는 미디어 항목 로드에 응답하여 미디어 플레이어 항목 이벤트를 발송합니다.
title: 로더 이벤트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 로더 이벤트{#loader-events}

TVSDK는 미디어 항목 로드에 응답하여 미디어 플레이어 항목 이벤트를 발송합니다.

이러한 이벤트는 대체 워크플로우를 제공합니다. MediaPlayer를 만들 때는 이 인터페이스를 구현할 필요가 없습니다. 다음 항목을 보유할 때 사용하십시오. `MediaPlayerItemLoader`.

미디어 플레이어 리소스 로드와 관련된 이벤트에 대한 알림을 받으려면 의 구현을 등록하십시오. `MediaPlayerItemLoader.LoaderListener` 다음 이벤트를 포함합니다.

| 이벤트 | 의미 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 미디어 리소스 로드가 완료되었습니다. |
| [오류 시](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 미디어 리소스를 로드하는 도중 문제가 발생했습니다. |

>[!NOTE]
>
>추가 정보 `onLoadInfo (loadInfo)` 를 클릭합니다.

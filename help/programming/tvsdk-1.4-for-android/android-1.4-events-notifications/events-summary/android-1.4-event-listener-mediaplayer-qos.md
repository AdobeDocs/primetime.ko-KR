---
description: TVSDK는 QoS(서비스 품질) 이벤트를 전달하여 버퍼링 또는 검색 등 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.
title: QoS 이벤트
exl-id: 0ccdaed1-1fce-46b7-b0f0-25e7ea98da86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# QoS 이벤트{#qos-events}

TVSDK는 QoS(서비스 품질) 이벤트를 전달하여 버퍼링 또는 검색 등 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.

모든 QoS 관련 이벤트에 대한 알림을 받으려면 의 구현을 등록하십시오. `MediaPlayer.QOSEventListener` 다음 콜백을 포함합니다.

| 이벤트 | 의미 |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | 버퍼링이 완료되었습니다. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | 버퍼링이 시작되었습니다. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | 조각이 정상적으로 다운로드되었습니다. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification. [경고](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) warning) | 복구할 수 있는 오류가 발생했습니다. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjustedTime) | 찾기가 완료되었습니다. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | 찾기를 시작하고 있습니다. |

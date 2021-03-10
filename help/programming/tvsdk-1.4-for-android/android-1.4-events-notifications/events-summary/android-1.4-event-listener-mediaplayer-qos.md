---
description: TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링이나 검색 등의 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.
title: QoS 이벤트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# QoS 이벤트{#qos-events}

TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링이나 검색 등의 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.

모든 QoS 관련 이벤트에 대한 알림을 받으려면 다음 콜백을 포함한 `MediaPlayer.QOSEventListener` 구현을 등록합니다.

| 이벤트 | 의미 |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | 버퍼링이 완료되었습니다. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | 버퍼링이 시작되었습니다. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | 조각이 성공적으로 다운로드되었습니다. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification. [경고 ](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) ) | 복구 가능한 오류가 발생했습니다. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjutedTime) | 검색 작업이 완료되었습니다. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | 검색 시작. |
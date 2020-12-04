---
description: 변형 재생 목록에 동일한 비트 전송률에 대한 여러 변환이 있고 변환 중 하나가 작동을 중지하면 장애 조치(failover) 처리가 발생합니다. TVSDK는 변환 간에 전환됩니다.
seo-description: 변형 재생 목록에 동일한 비트 전송률에 대한 여러 변환이 있고 변환 중 하나가 작동을 중지하면 장애 조치(failover) 처리가 발생합니다. TVSDK는 변환 간에 전환됩니다.
seo-title: 장애 조치
title: 장애 조치
uuid: 064886ab-afa2-4afc-b795-d094b31934b8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# 페일오버 {#failover}

변형 재생 목록에 동일한 비트 전송률에 대한 여러 변환이 있고 변환 중 하나가 작동을 중지하면 장애 조치(failover) 처리가 발생합니다. TVSDK는 변환 간에 전환됩니다.

다음 예는 장애 조치(failover) URL이 동일한 비트 속도의 변형 재생 목록을 보여줍니다.

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

TVSDK가 변형 재생 목록을 로드하면 동일한 비트 전송률에 대한 컨텐츠의 모든 변환에 대한 URL을 포함하는 큐를 만듭니다. URL 요청이 실패하면 TVSDK는 장애 조치 큐에서 동일한 비트 속도의 다음 URL을 사용합니다. 특정 실패 시 TVSDK는 제대로 작동하는 URL을 찾거나 사용 가능한 모든 URL을 시도하기 전까지 사용 가능한 모든 URL을 한 번 순환합니다. TVSDK가 사용 가능한 모든 URL을 시도했지만 URL이 작동하지 않으면 TVSDK가 컨텐츠 재생을 중단합니다.

페일오버는 M3U8 수준에서만 실행되며, 이는 다음을 의미합니다.

* VOD의 경우 재생이 시작된 이후가 아니라 재생을 시작한 경우에만 장애 조치(failover)가 발생할 수 있습니다.
* 실시간 스트리밍의 경우 스트림 중간에 장애 조치가 발생할 수 있습니다.

>[!TIP]
>
>Apple AV Foundation 플레이어가 아닌 TVSDK는 장애 조치 처리를 제공합니다.
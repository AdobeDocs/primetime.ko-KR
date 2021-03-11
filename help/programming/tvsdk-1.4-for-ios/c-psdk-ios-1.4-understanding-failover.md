---
description: 변형 재생 목록에 동일한 비트 전송률에 대한 여러 변환이 있고 변환 중 하나가 작동을 중단할 때 장애 조치(failover) 처리가 발생합니다. TVSDK는 변환 간에 전환됩니다.
title: 페일오버
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# 장애 조치(failover){#failover}

변형 재생 목록에 동일한 비트 전송률에 대한 여러 변환이 있고 변환 중 하나가 작동을 중단할 때 장애 조치(failover) 처리가 발생합니다. TVSDK는 변환 간에 전환됩니다.

다음 예제에서는 장애 조치(failover) URL이 같은 비트 전송률을 갖는 변형 재생 목록을 보여 줍니다.

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

TVSDK가 변형 재생 목록을 로드하면 동일한 비트 전송률에 대한 모든 컨텐츠 변환에 대한 URL이 들어 있는 대기열이 만들어집니다. URL 요청이 실패하면 TVSDK는 장애 조치 큐에서 동일한 비트 전송률의 다음 URL을 사용합니다. 특정 실패 시 TVSDK는 제대로 작동하는 URL을 검색하거나 사용 가능한 모든 URL을 시도하기 전까지 사용 가능한 모든 URL을 한 번 반복합니다. TVSDK가 사용 가능한 모든 URL을 시도했지만 URL이 작동하지 않는 경우 TVSDK는 컨텐츠 재생을 중단합니다.

페일오버 기능은 M3U8 수준에서만 발생합니다. 즉, 다음과 같습니다.

* VOD의 경우 재생이 시작된 이후가 아니라 재생을 시작할 때만 장애 조치(failover)가 발생할 수 있습니다.
* 실시간 스트리밍의 경우 스트림 중간에 장애 조치가 발생할 수 있습니다.

>[!TIP]
>
>Apple AV Foundation 플레이어가 아닌 TVSDK는 페일오버 처리를 제공합니다.


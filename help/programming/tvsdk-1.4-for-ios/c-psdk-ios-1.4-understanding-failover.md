---
description: 변형 재생 목록에 동일한 비트율에 대한 여러 변환이 있고 변환 중 하나가 작동을 중지하면 장애 조치 처리가 발생합니다. TVSDK는 렌디션 간에 전환합니다.
title: 페일오버
exl-id: 8c215e2b-e601-4991-a66f-0e810176a511
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 페일오버{#failover}

변형 재생 목록에 동일한 비트율에 대한 여러 변환이 있고 변환 중 하나가 작동을 중지하면 장애 조치 처리가 발생합니다. TVSDK는 렌디션 간에 전환합니다.

다음 예제에서는 동일한 비트율의 장애 조치(failover) URL을 가진 변형 재생 목록을 보여줍니다.

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

TVSDK는 변형 재생 목록을 로드할 때 동일한 비트 전송률에 대한 콘텐츠의 모든 렌디션에 대한 URL을 포함하는 큐를 만듭니다. URL 요청이 실패하면 TVSDK는 장애 조치 큐에서 동일한 비트 전송률의 다음 URL을 사용합니다. 특정 실패 시간에 TVSDK는 올바르게 작동하는 URL을 찾거나 사용 가능한 URL을 모두 시도할 때까지 사용 가능한 모든 URL을 한 번 순환합니다. TVSDK에서 사용 가능한 모든 URL을 시도했지만 URL이 하나도 작동하지 않는 경우 TVSDK는 콘텐츠 재생 시도를 중단합니다.

페일오버는 M3U8 수준에서만 발생하며, 이는 다음을 의미합니다.

* VOD의 경우 페일오버는 재생을 시작한 후가 아니라 재생을 시작할 때만 발생할 수 있습니다.
* 라이브 스트리밍의 경우 스트림 중간에 장애 조치가 발생할 수 있습니다.

>[!TIP]
>
>Apple AV Foundation 플레이어가 아닌 TVSDK는 장애 조치(failover) 처리를 제공합니다.

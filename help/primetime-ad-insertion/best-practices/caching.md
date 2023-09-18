---
title: 캐싱
description: 캐싱
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP 캐싱 {#caching}

Primetime Ad Insertion은 광고 크리에이티브와 컨텐츠를 가져올 때 기본적으로 HTTP 캐시 제어 헤더를 준수합니다.  이렇게 하면 Primetime Ad Insertion이 모든 클라이언트에서 CDN에 대해 수행하는 데 필요한 네트워크 요청의 양을 크게 줄일 수 있습니다.  캐싱을 위해 Adobe은 다음 설정을 권장하며 HTTP 헤더 전송을 포함합니다 `max-age` cdn에서.  비디오 스트림 및 광고 스트림에서 이러한 헤더를 활성화하려면 CDN 담당자에게 문의하십시오.

## 라이브/선형 콘텐츠의 경우 {#caching-live-linear-content}

* 기본 매니페스트: 24시간 또는 Cache-Control: max-age=86400
* Media manifest: 1초 또는 Cache-Control: max-age=1

## VOD 콘텐츠의 경우 {#caching-vod-content}

* 기본 매니페스트: 24시간 또는 Cache-Control: max-age=86400
* Media manifest: 24시간 또는 Cache-Control: max-age=86400

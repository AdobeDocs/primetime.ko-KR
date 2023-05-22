---
description: 일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS/DASH와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS)/DASH(Dynamic Adaptive Streaming over HTTP) 콘텐츠 스트림에 결합할 수 없습니다. Adobe Primetime 광고 삽입 및 브라우저 TVSDK는 호환되지 않는 비디오를 호환되는 m3u8/mpd 비디오로 다시 패키지(코드 변환)할 수 있습니다.
title: 호환되지 않는 광고 다시 패키지(코드 변환)
exl-id: aaa78d5a-4b4b-4d50-b516-d39b47174487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 호환되지 않는 광고 다시 패키지(코드 변환){#repackage-transcode-incompatible-ads}

일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS/DASH와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS)/DASH(Dynamic Adaptive Streaming over HTTP) 콘텐츠 스트림에 결합할 수 없습니다. Adobe Primetime 광고 삽입 및 브라우저 TVSDK는 호환되지 않는 비디오를 호환되는 m3u8/mpd 비디오로 다시 패키지(코드 변환)할 수 있습니다.

에이전시 광고 서버, 인벤토리 파트너 또는 광고 네트워크와 같은 다양한 타사에서 제공하는 광고는 종종 점진적 다운로드 MP4와 같은 호환되지 않는 형식으로 전달됩니다.

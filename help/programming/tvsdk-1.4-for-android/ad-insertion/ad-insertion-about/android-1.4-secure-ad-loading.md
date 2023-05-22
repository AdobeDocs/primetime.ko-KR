---
title: HTTPS를 통한 보안 광고 로드
description: HTTPS를 통한 보안 광고 로드
copied-description: true
exl-id: e12cb9d4-05d4-485e-b629-1af680b83e04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# HTTPS를 통한 보안 광고 로드{#secure-ad-loading-over-https}

Adobe Primetime은 Primetime 광고 서버에 대한 첫 번째 호출 및 HTTPS를 통한 CRS 관련 호출을 요청하는 옵션을 제공합니다.

이 기능은 기본적으로 활성화되어 있지 않습니다. 보안 광고 로드를 활성화하려면 다음을 사용하십시오.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

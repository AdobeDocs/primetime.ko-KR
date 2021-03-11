---
title: HTTPS를 통한 안전한 광고 로딩
description: HTTPS를 통한 안전한 광고 로딩
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# HTTPS {#secure-ad-loading-over-https}를 통해 안전한 광고 로드

Adobe Primetime은 HTTPS를 통해 Primetime 광고 서버 및 CRS 관련 호출에 처음으로 요청하는 옵션을 제공합니다.

이 기능은 기본적으로 활성화되지 않습니다. 보안 광고 로드를 활성화하려면 다음을 사용하십시오.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

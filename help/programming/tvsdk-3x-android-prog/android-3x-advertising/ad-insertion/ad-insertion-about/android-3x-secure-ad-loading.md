---
description: 'null'
seo-description: 'null'
seo-title: HTTPS를 통한 안전한 광고 로딩
title: HTTPS를 통한 안전한 광고 로딩
uuid: 18be77cc-c59b-4982-b8c1-e4451495edd2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# HTTPS {#secure-ad-loading-over-https}를 통해 안전한 광고 로딩

Adobe Primetime은 HTTPS를 통해 Primetime 광고 서버와 CRS 관련 전화에 대한 첫 번째 호출을 요청할 수 있는 옵션을 제공합니다.

이 기능은 기본적으로 활성화되어 있지 않습니다. 보안 광고 로드를 활성화하려면 다음을 사용하십시오.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

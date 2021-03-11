---
title: HTTPS를 통한 안전한 광고 로딩
description: HTTPS를 통한 안전한 광고 로딩
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# HTTPS{#secure-ad-loading-over-https}를 통해 안전한 광고 로드

Adobe Primetime은 플레이어가 http에서 호스팅된 경우에도 https를 통해 타사 광고 서버를 요청할 수 있습니다. Auditude Ad 해결 프로그램 단계 동안 클라이언트가 검색하는 https로 해당 광고 서버 호출만 업그레이드됩니다.

>[!NOTE]
>
>이 기능은 Flash에서 지원되지 않습니다.

보안 광고 로드를 활성화하려면 다음을 사용하십시오. 기본적으로 활성화되지 않습니다.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```

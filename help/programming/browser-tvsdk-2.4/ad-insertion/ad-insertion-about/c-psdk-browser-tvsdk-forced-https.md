---
title: HTTPS를 통한 보안 광고 로드
description: HTTPS를 통한 보안 광고 로드
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# HTTPS를 통한 보안 광고 로드{#secure-ad-loading-over-https}

Adobe Primetime은 플레이어가 http에서 호스팅되는 경우에도 https를 통해 서드파티 광고 서버를 요청할 수 있습니다. 광고 서버 호출만 Auditude Ad Resolver 단계 중에 클라이언트가 검색하는 https로 업그레이드됩니다.

>[!NOTE]
>
>이 기능은 Flash 시 지원되지 않습니다.

보안 광고 로드를 활성화하려면 다음을 사용하십시오. 기본적으로 활성화되어 있지 않습니다.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```

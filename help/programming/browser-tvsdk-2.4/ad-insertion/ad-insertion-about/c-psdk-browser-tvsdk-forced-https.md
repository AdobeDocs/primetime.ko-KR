---
description: 'null'
seo-description: 'null'
seo-title: HTTPS를 통한 안전한 광고 로딩
title: HTTPS를 통한 안전한 광고 로딩
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---


# HTTPS{#secure-ad-loading-over-https}를 통해 안전한 광고 로딩

Adobe Primetime은 플레이어가 http에서 호스팅되더라도 https를 통해 타사 광고 서버를 요청할 수 있습니다. Auditude Ad 확인자 단계 동안 클라이언트가 찾는 https로 해당 광고 서버 호출만 업그레이드됩니다.

>[!NOTE]
>
>이 기능은 Flash에서 지원되지 않습니다.

보안 광고 로드를 활성화하려면 다음을 사용하십시오. 기본적으로 활성화되지 않습니다.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```

---
description: 'null'
seo-description: 'null'
seo-title: HTTPS를 통한 안전한 광고 로딩
title: HTTPS를 통한 안전한 광고 로딩
uuid: 72ab94d3-ee0c-4f02-adf2-c186ae6aec26
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# HTTPS를 통한 안전한 광고 로딩 {#secure-ad-loading-over-https}

Adobe Primetime은 HTTPS를 통해 Primetime 광고 서버 및 CRS 관련 호출에 처음으로 요청할 수 있는 옵션을 제공합니다.

이 기능은 기본적으로 활성화되어 있지 않습니다. 보안 광고 로드를 활성화하려면 다음을 사용하십시오.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```


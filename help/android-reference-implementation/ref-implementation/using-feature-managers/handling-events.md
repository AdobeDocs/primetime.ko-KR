---
description: 애플리케이션이 기능 관리자에서 발송한 이벤트를 처리해야 하는 경우 PlayerFragment.java 파일에 관리자를 등록해야 합니다.
title: 이벤트 처리
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 이벤트 처리 {#handling-events}

애플리케이션이 기능 관리자에서 발송한 이벤트를 처리해야 하는 경우 PlayerFragment.java 파일에 관리자를 등록해야 합니다.

예:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```

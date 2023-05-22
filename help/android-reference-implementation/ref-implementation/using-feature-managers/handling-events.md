---
description: 애플리케이션이 기능 관리자에서 발송한 이벤트를 처리해야 하는 경우 PlayerFragment.java 파일에 관리자를 등록해야 합니다.
title: 이벤트 처리
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

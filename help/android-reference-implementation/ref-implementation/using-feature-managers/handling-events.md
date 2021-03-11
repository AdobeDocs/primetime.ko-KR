---
description: 응용 프로그램이 기능 관리자에서 전달된 이벤트를 처리해야 하는 경우 PlayerFragment.java 파일에서 관리자를 등록해야 합니다.
title: 이벤트 처리
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# 이벤트 처리 {#handling-events}

응용 프로그램이 기능 관리자에서 전달된 이벤트를 처리해야 하는 경우 PlayerFragment.java 파일에서 관리자를 등록해야 합니다.

예:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```

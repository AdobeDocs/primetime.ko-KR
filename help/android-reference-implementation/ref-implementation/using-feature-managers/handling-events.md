---
description: 응용 프로그램이 기능 관리자에서 전달된 이벤트를 처리해야 하는 경우 PlayerFragment.java 파일에서 관리자를 등록해야 합니다.
seo-description: 응용 프로그램이 기능 관리자에서 전달된 이벤트를 처리해야 하는 경우 PlayerFragment.java 파일에서 관리자를 등록해야 합니다.
seo-title: 이벤트 처리
title: 이벤트 처리
uuid: 13639f02-0dcc-4a0a-8524-515da5478006
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

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

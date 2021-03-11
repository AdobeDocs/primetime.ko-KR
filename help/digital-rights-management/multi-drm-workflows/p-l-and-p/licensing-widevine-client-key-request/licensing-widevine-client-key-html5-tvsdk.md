---
description: 코드는 DRMManager를 통해 키를 요청할 수 있습니다.
title: HTML5 TVSDK의 주요 요청 워크플로우
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# HTML5 TVSDK{#key-request-workflow-on-html-tvsdk}의 주요 요청 워크플로우

코드는 DRMManager를 통해 키를 요청할 수 있습니다.

브라우저 TV SDK는 DRMManager 객체를 통해 setProtectionData API도 표시합니다.

```
[  /** 
   * This will only work for MSE. 
   * <p> Attach key system specific data to use for DRM 
license acquisition. </p> 
   * @param {Object} protectionData - an object containing property names corresponding to key system name strings 
   * (e.g. "org.w3.clearkey") and associated values being instances of 
   * MediaPlayer.vo.protection.ProtectionData. 
   * @returns {AdobePSDK.PSDKErrorCode} kECSuccess or one of the error codes. 
   * @function 
   * @memberof AdobePSDK.DRMManager# 
   */ 
   setProtectionData: function(protectionData) 
```

일반적인 방식으로 컨텐츠 재생을 시작하기 전에 코드가 이 API를 호출해야 합니다. MediaPlayer.vo.protection.ProtectionData는 여기에 문서화되어 있습니다.[https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html](https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html)

다음은 PlayReady 및 Widevine 모두에 대한 라이센스 서버 URL이 있는 샘플 보호 데이터 개체입니다.

```
var protectionData = { 
   "com.widevine.alpha": { 
                          "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/ 
                           ?ExpressPlayToken=AQAAABIDKA4AAABQuPPoebWWZZD2l3APRKkkagEDOXm 
                           CjgbhsqJTYeZ9KabkjCvSLvuXGHiVLymBnouGXDdCKpbz5IvB3jCZp9U05pys 
                           l9eavucsWXnA0tafbM-1SSJKXOa70kvxAJ_ybhdcmy7-6g" 
                          }, 
   "com.microsoft.playready": { 
                               "serverURL": "https://expressplay-licensing.axprod.net/ 
                                LicensingService.ashx?ExpressPlayToken=AQAAAw_ZXqcAAAB 
                                gHD1gnn_AMQJKfFCP3k9zbBw2srzBLryJVLXclnjhcSBCz4TBzrtfe 
                                gmSw1hAKdFHTNL-KVBGsI4ygBnfPRBUCvGsVOwpQ944fhq45W06ygJ 
                                roB2xOrM03tbkWcrthI7y_UQdHzufHjcBqKZm8QDoqKpxrxc" 
                               } 
   };
```

각 브라우저는 하나의 DRM 시스템만 지원하므로 TVSDK는 특정 DRM 시스템을 강제하는 API를 제공하지 않습니다.

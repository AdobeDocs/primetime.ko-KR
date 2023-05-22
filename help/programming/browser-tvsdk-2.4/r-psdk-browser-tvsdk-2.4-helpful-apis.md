---
description: Adobe Flash Player 사용에 도움이 될 수 있는 몇 가지 API가 있습니다.
title: Adobe Flash Player에 유용한 API
exl-id: 3a80088b-382e-4624-bbaa-6d7e9f0126e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---

# Adobe Flash Player에 유용한 API{#helpful-apis-for-the-adobe-flash-player}

Adobe Flash Player 사용에 도움이 될 수 있는 몇 가지 API가 있습니다.

## AdobePSDK.MediaResource {#section_8C339FA1386D4B1A926A1459B2619E5E}

```js
new MediaResource(url, type, metadata, forceFlash)
```

지원되는 경우 `forceFlash` 재생 기술 결정 시퀀스를 재정의하고 구현이 Flash Player을 사용하도록 하는 매개 변수입니다.

<!--<a id="section_FEE3205B532446498771F7DD55B5E79F"></a>-->

```js
AdobePSDK.PlayerTechnology = { 
/** 
* Determine the {AdobePSDK.PlayerTechnology} that would be used for the given 
* media resource. 
* @param {AdobePSDK.MediaResource} mediaResource 
* @returns {AdobePSDK.PlayerTechnology.Type} 
*/ 
getSupportedTechnology(mediaResource); 
}; 
 
AdobePSDK.PlayerTechnology.Type = {  
MSE, 
VIDEO_TAG,  
FLASH,  
UNKNOWN 
}; 
 
/** 
* Set the path to the SWF relative to the main html page or using http URL. 
* Defaults to the current directory of the html page. 
* 
* @param swfPath 
*/ 
AdobePSDK.setSWFPath(swfPath); 
 
/** 
* Set the path to the folder containing the authorization token(s). 
* If not set, defaults to the token folder within the SWFPath: SWFPath + "token/". 
* @param authorizationTokenPath 
*/ 
AdobePSDK.setAuthorizationTokenPath(authorizationTokenPath); 
 
/** 
* Set the name of the authorization token file. Defaults to "hlsAF_localhost.dat". 
* @param authorizationTokenFileName 
*/ 
AdobePSDK.setAuthorizationTokenFilename(authorizationTokenFilename); 
 
/** 
* Set the authorization token type, can be "SWF" or "DAT". Defaults to "DAT" 
* @param {String} authorizationTokenType 
*/ 
AdobePSDK.setAuthorizationTokenType(authorizationTokenType);
```

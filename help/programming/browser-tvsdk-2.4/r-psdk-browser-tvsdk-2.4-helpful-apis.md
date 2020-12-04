---
description: Adobe Flash Player을 사용하는 데 도움이 되는 일부 API가 있습니다.
seo-description: Adobe Flash Player을 사용하는 데 도움이 되는 일부 API가 있습니다.
seo-title: Adobe Flash Player에 대한 유용한 API
title: Adobe Flash Player에 대한 유용한 API
uuid: eae314c0-fd9e-480f-ae1c-9b5f3eb4db4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---


# Adobe Flash Player{#helpful-apis-for-the-adobe-flash-player}에 대한 유용한 API

Adobe Flash Player을 사용하는 데 도움이 되는 일부 API가 있습니다.

## AdobePSDK.MediaResource {#section_8C339FA1386D4B1A926A1459B2619E5E}

```js
new MediaResource(url, type, metadata, forceFlash)
```

지원되는 경우 `forceFlash` 매개 변수를 사용하여 재생 기술 결정 시퀀스를 재정의하고 구현에서 Flash Player을 사용하도록 할 수 있습니다.

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


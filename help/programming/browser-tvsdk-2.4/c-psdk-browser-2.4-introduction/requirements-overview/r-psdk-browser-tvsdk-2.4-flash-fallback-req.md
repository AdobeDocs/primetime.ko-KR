---
description: Flash Player을 사용하려면 환경이 필요한 요구 사항을 충족하는지 확인하십시오.
title: Flash Player 요구 사항
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Flash Player 요구 사항{#flash-player-requirements}

Flash Player을 사용하려면 환경이 필요한 요구 사항을 충족하는지 확인하십시오.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

다음은 Flash Player의 요구 사항입니다.

* `Primetime.js`으로 재생하려면 Flash Player 버전 23을 적어도 설치하십시오.
* Flash Player 버전 23 이상을 업데이트할지 여부를 묻는 메시지가 나타나면 Flash Player 버전 11.0.0 이상을 설치하십시오.

## 패키징 요구 사항 {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

Flash Player을 사용하여 재생하려면 다음 SWF 파일이 필요합니다.

* 브라우저 TVSDK API를 처리하는 기본 응용 프로그램 SWF 파일입니다.
* Flash Player 설치 및 업데이트를 처리하는 `playerProductInstall.swf` SWF 파일.

또한 Flash에서 비디오를 재생하려면 SWF 또는 `.DAT` 파일일 수 있는 인증 토큰 파일이 필요합니다. SWF 파일의 경로, 인증 토큰 파일, 토큰 파일 이름 및 유형은 Adobe PSDK API를 사용하여 지정할 수 있습니다.

예:

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```


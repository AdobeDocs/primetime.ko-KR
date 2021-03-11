---
description: 브라우저 TVSDK는 FairPlay, PlayReady, Widevine 등 다른 DRM 솔루션으로 보호되는 콘텐츠를 재생하는 데 사용할 수 있는 DRM 인터페이스를 제공합니다.
title: DRM 인터페이스 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# DRM 인터페이스 개요{#drm-interface-overview}

브라우저 TVSDK는 FairPlay, PlayReady, Widevine 등 다른 DRM 솔루션으로 보호되는 콘텐츠를 재생하는 데 사용할 수 있는 DRM 인터페이스를 제공합니다.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM 지원은 Microsoft PlayReady(Windows 8.1 및 Edge의 Internet Explorer) 및 Widevine(Google Chrome) DRM 시스템으로 보호되는 MPEG-Dash 스트림에 사용할 수 있습니다. DRM 지원은 FairPlay로 보호되는 Safari의 HLS 스트림에 대해 사용할 수 있습니다.

DRM 워크플로우의 주요 인터페이스는 `DRMManager`입니다. `DRMManager` 인스턴스에 대한 참조를 MediaPlayer 인스턴스를 통해 얻을 수 있습니다.

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

DRM으로 보호된 콘텐츠의 고급 재생 워크플로우는 다음과 같습니다.

1. 브라우저 TVSDK가 보호된 스트림의 라이선스 획득 프로세스에서 사용할 DRM 시스템 특정 데이터를 첨부하려면 `mediaPlayer.replaceCurrentResource`을(를) 호출하기 전에 다음 호출을 수행하십시오.

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. 동일한 콘텐츠가 다른 브라우저에서 서로 다른 DRM 시스템에서 작동될 것으로 예상되는 경우 여러 DRM 시스템에 대해 보호 데이터를 지정할 수 있습니다.

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
   
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. 보호 데이터가 설정되지 않으면 해당되는 경우 DRM 시스템에 대한 PSSH 상자에서 라이센스 URL과 같은 필요한 정보가 검색됩니다.

   >[!TIP]
   >
   >보호 데이터를 지정하면 PSSH 상자에 지정된 라이센스 URL이 무시됩니다.

1. 기본적으로 DRM 라이센스의 세션 유형은 일시적이며 세션이 닫힌 후 라이센스가 저장되지 않습니다.

   `DRMManager`의 API를 사용하여 세션 유형을 지정할 수 있습니다.  이전 버전과의 호환성을 위해 세션 유형에는 `temporary`, `persistent-license`, `persistent-usage-record` 및 `persistent`이 포함됩니다.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. 사용된 `sessionType`이 `persistent-license` 또는 `persistent`인 경우 `DRMManager.returnLicense`를 호출하여 DRM 라이센스를 반환할 수 있습니다.

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
   
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
   
   drmManager = mediaPlayer.drmManager; 
   
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```


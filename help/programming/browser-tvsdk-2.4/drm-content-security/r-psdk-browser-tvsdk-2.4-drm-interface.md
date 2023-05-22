---
description: 브라우저 TVSDK는 FairPlay, PlayReady 및 Widevine을 비롯한 다양한 DRM 솔루션으로 보호되는 콘텐츠를 재생하는 데 사용할 수 있는 DRM 인터페이스를 제공합니다.
title: DRM 인터페이스 개요
exl-id: aa13f042-4472-4fc3-b7ba-61746b8e024a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# DRM 인터페이스 개요{#drm-interface-overview}

브라우저 TVSDK는 FairPlay, PlayReady 및 Widevine을 비롯한 다양한 DRM 솔루션으로 보호되는 콘텐츠를 재생하는 데 사용할 수 있는 DRM 인터페이스를 제공합니다.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM 지원은 Microsoft PlayReady(Windows 8.1 및 Edge의 Internet Explorer) 및 Widevine(Google Chrome의) DRM 시스템으로 보호된 MPEG-Dash 스트림에 사용할 수 있습니다. DRM 지원은 FairPlay로 보호되는 Safari의 HLS 스트림에 사용할 수 있습니다.

DRM 워크플로의 키 인터페이스는 `DRMManager`. 에 대한 참조 `DRMManager` 인스턴스는 MediaPlayer 인스턴스를 통해 가져올 수 있습니다.

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

다음은 DRM 보호 콘텐츠 재생을 위한 높은 수준의 워크플로우입니다.

1. 보호된 스트림에 대한 라이선스 획득 프로세스에서 브라우저 TVSDK가 사용할 DRM 시스템 관련 데이터를 첨부하려면 호출하기 전에 다음 호출을 수행하십시오 `mediaPlayer.replaceCurrentResource`:

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

1. 동일한 콘텐츠가 서로 다른 브라우저에서 서로 다른 DRM 시스템에서 작동할 것으로 예상되면 여러 DRM 시스템에 대해 보호 데이터를 지정할 수 있습니다.

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

1. 보호 데이터가 설정되지 않은 경우, 라이센스 URL과 같은 필수 정보는 해당되는 경우 DRM 시스템용 PSSH 상자에서 검색됩니다.

   >[!TIP]
   >
   >보호 데이터를 지정하면 PSSH 상자에 지정된 라이선스 URL이 재정의됩니다.

1. 기본적으로 DRM 라이선스의 세션 유형은 임시입니다. 즉, 세션이 닫힌 후에는 라이선스가 저장되지 않습니다.

   에서 API를 사용하여 세션 유형을 지정할 수 있습니다 `DRMManager`.  이전 버전과의 호환성을 위해 세션 유형은 다음과 같습니다. `temporary`, `persistent-license`, `persistent-usage-record`, 및 `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. 다음의 경우 `sessionType` 사용됨 `persistent-license` 또는 `persistent`를 호출하여 DRM 라이센스를 반환할 수 있습니다. `DRMManager.returnLicense`.

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

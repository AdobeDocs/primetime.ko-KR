---
description: 다음 새로운 API를 사용하여 DRM 콜백을 정의할 수 있습니다.
seo-description: 다음 새로운 API를 사용하여 DRM 콜백을 정의할 수 있습니다.
seo-title: DRM 콜백 구현
title: DRM 콜백 구현
uuid: a54c5ec2-299f-47b0-b65b-eed5656ab6aa
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# DRM 콜백 구현{#implementing-drm-callbacks}

다음 새로운 API를 사용하여 DRM 콜백을 정의할 수 있습니다.

<!--<a id="section_1090BFDB2C1D4EA4AAC9F9A6EC9DCD51"></a>-->

호출 백 함수(예: `parseContentIdCallback`)를 정의하여 컨텐츠 ID를 구문 분석하고 API를 사용하여 `drmManager` 설정할 수 `setParseContentIdCallback` 있습니다.

```js
var arrayToString = function (array) { 
        var uint16array = new Uint16Array(array.buffer); 
        return String.fromCharCode.apply(null, uint16array); 
}, 
  
parseContentIdCallback = function (initData) { 
        var contentId = arrayToString(initData), 
            tokens = contentId?contentId.split('/'):[]; 
        if(tokens.length) { 
            return tokens[tokens.length-1]; 
        } else { 
            return ''; 
        } 
}; 
   
drmManager.setParseContentIdCallback(parseContentIdCallback);
```

<!--<a id="section_1E082B428EA74D9CA11C052158A83947"></a>-->

콜백 함수(예: `onCertificateResponseCallback`)를 정의하여 텍스트 인증서 응답을 처리하고 API를 사용하여 함수를 `drmManager` 로 설정할 수 `setCertificateResponseCallback` 있습니다. 기본 동작을 `setCertificateResponseCallback` 무시하도록 설정할 수 있습니다. 예를 들어, `certificateResponseType` 다른 `ArrayBuffer`콜백이 있는 경우 이 콜백을 사용하여 인증서 응답을 `ArrayBuffer` 유형으로 변환할 수 있습니다.

```js
var base64DecodeUint8Array = function (input) { 
        var raw = window.atob(input); 
        var rawLength = raw.length; 
        var array = new Uint8Array(new ArrayBuffer(rawLength)); 
 
        for (var i = 0; i < rawLength; i++) 
            array[i] = raw.charCodeAt(i); 
 
        return array; 
    }, 
  
onCertificateResponseCallback = function (certificateResponse) { 
    if(certificateResponse) { 
        var certText = certificateResponse.trim(); 
        certText = certText.replace(/^"(.+(?="$))"$/, '$1'); 
        return base64DecodeUint8Array(certText); 
    } 
}; 
  
drmManager.setCertificateResponseCallback(onCertificateResponseCallback);
```

<!--<a id="section_4DCC1B3ABCED484EB5340A558C9A770A"></a>-->

콜백 함수를 정의하여 라이센스 메시지와 라이센스 응답을 구문 분석하여 콜로 전달할 수 `drmManager.acquireLicense`있습니다. `onLicenseResponseCallback` 는 API의 새 매개 `acquireLicense` 변수입니다.

```js
var base64EncodeUint8Array = function (input) { 
        var keyStr = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/="; 
        var output = ""; 
        var chr1, chr2, chr3, enc1, enc2, enc3, enc4; 
        var i = 0; 
        while (i < input.length) { 
            chr1 = input[i++]; 
            chr2 = i < input.length ? input[i++] : Number.NaN; // Not sure if the index 
            chr3 = i < input.length ? input[i++] : Number.NaN; // checks are needed here 
  
            enc1 = chr1 >> 2; 
            enc2 = ((chr1 & 3) << 4) | (chr2 >> 4); 
            enc3 = ((chr2 & 15) << 2) | (chr3 >> 6); 
            enc4 = chr3 & 63; 
  
            if (isNaN(chr2)) { 
                enc3 = enc4 = 64; 
            } else if (isNaN(chr3)) { 
                enc4 = 64; 
            } 
            output += keyStr.charAt(enc1) + keyStr.charAt(enc2) + 
                keyStr.charAt(enc3) + keyStr.charAt(enc4); 
        } 
        return output; 
    }, 
  
    base64DecodeUint8Array = function (input) { 
        var raw = window.atob(input); 
        var rawLength = raw.length; 
        var array = new Uint8Array(new ArrayBuffer(rawLength)); 
  
        for (var i = 0; i < rawLength; i++) 
            array[i] = raw.charCodeAt(i); 
  
        return array; 
    }, 
  
    onLicenseMessageCallback = function (drmLicenseRequest) { 
        var licenseMessage = drmLicenseRequest.licenseMessage, 
            base64Message = base64EncodeUint8Array(licenseMessage); 
        return base64Message; 
    }, 
  
    onLicenseResponseCallback = function (serverResponse) { 
        var keyText = serverResponse.licenseResponse.trim(); 
        keyText = keyText.replace(/^"(.+(?="$))"$/, '$1'); 
        return base64DecodeUint8Array(keyText); 
    };

drmManager.acquireLicense(drmMetadata, null, acquireLicenseListener, onLicenseMessageCallback, onLicenseResponseCallback);
```

보호 데이터에서 새 **[!UICONTROL certificateResponseType]** 필드를 사용하여 인증서 응답 유형을 설정합니다. 다음은 보호 데이터의 예입니다.

```js
{ 
     "com.apple.fps.1_0": { 
         "serverURL": "https://fairplay.license.istreamplanet.com/api/license/9d3ed760-3ba9-4042-b4a4-07e0d8069200", 
         "certificateURL":"https://fairplay-stage.license.istreamplanet.com/api/AppCert/9d3ed760-3ba9-4042-b4a4-07e0d8069200", 
         "licenseResponseType": "text", 
         "certificateResponseType": "text", 
         "httpRequestHeaders": { 
            "Content-type": "application/x-www-form-urlencoded" 
         } 
     } 
}
```

필드 `certificateResponseType` 사용은 선택 사항입니다. 이 값을 사용하지 않는 경우 이 값은 로 `ArrayBuffer`간주됩니다.

---
description: 브라우저 TVSDK는 현재 매니페스트 및 조각에 확장이 없는 스트림 재생을 지원합니다.
title: 확장 없는 스트림
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# 확장 없는 스트림{#extensionless-streams}

브라우저 TVSDK는 현재 매니페스트 및 조각에 확장이 없는 스트림 재생을 지원합니다.

## 조각 수준 {#section_0E035129501D4A77BBC14192D8A53A86}

브라우저 TVSDK는 응답의 처음 몇 바이트를 구문 분석하여 확장자가 없는 부분의 콘텐츠 유형을 검색합니다. 유효한 콘텐츠 유형이 검색되지 않는 경우 브라우저 TVSDK에서 오류가 발생합니다.

## 매니페스트 수준 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

브라우저 TVSDK는 `replaceCurrentResource` 메서드에서 전달되는 `mediaResource.resourceType` 매개 변수를 사용하여 매니페스트 URL의 콘텐츠 유형을 감지합니다. 자세한 내용은 `AdobePSDK.MediaPlayer` 클래스를 참조하십시오.

UI 프레임워크 플레이어에서 다음과 같이 미디어 리소스의 리소스 유형을 지정할 수 있습니다.

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 
```

`resourceType`을(를) 제공하지 않으면 UI 프레임워크는 리소스 URL 확장의 리소스 유형을 결정합니다. 이 확장명은 `replaceCurrentResource` 메서드로 전달됩니다.

>[!TIP]
>
>확장 없는 매니페스트의 경우 UI 프레임워크에서 리소스를 로드하는 동안 `resourceType`이 항상 전달되는지 확인하십시오.


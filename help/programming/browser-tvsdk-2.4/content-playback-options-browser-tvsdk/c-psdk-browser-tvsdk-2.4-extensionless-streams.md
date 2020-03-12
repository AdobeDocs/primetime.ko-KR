---
description: 브라우저 TVSDK는 현재 매니페스트 및 조각에 익스텐션이 포함되지 않은 스트림의 재생을 지원합니다.
seo-description: 브라우저 TVSDK는 현재 매니페스트 및 조각에 익스텐션이 포함되지 않은 스트림의 재생을 지원합니다.
seo-title: 확장 기능 없는 스트림
title: 확장 기능 없는 스트림
uuid: c69ba62b-a940-4211-920d-2e559849fd6d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 확장 기능 없는 스트림{#extensionless-streams}

브라우저 TVSDK는 현재 매니페스트 및 조각에 익스텐션이 포함되지 않은 스트림의 재생을 지원합니다.

## 조각 수준 {#section_0E035129501D4A77BBC14192D8A53A86}

Browser TVSDK는 응답의 처음 몇 바이트를 구문 분석하여 익스텐션이 없는 부분의 컨텐츠 유형을 검색합니다. 올바른 콘텐츠 유형이 검색되지 않으면 브라우저 TVSDK에서 오류가 발생합니다.

## 매니페스트 수준 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

브라우저 TVSDK는 `mediaResource.resourceType` `replaceCurrentResource` 메서드에서 전달되는 매개 변수를 사용하여 매니페스트 URL의 콘텐츠 형식을 검색합니다. 자세한 내용은 `AdobePSDK.MediaPlayer` 클래스를 참조하십시오.

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

제공되지 `resourceType` 않는 경우 UI 프레임워크는 리소스 URL 확장의 리소스 유형을 결정한 다음 `replaceCurrentResource` 메서드에 전달됩니다.

>[!TIP]
>
>확장 없는 매니페스트의 경우 UI 프레임워크에서 리소스를 로드하는 동안 항상 `resourceType` 전달되는지 확인하십시오.


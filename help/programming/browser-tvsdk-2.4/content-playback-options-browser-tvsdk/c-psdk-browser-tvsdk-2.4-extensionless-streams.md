---
description: 브라우저 TVSDK는 현재 매니페스트 및 조각에 확장이 포함되지 않은 스트림 재생을 지원합니다.
title: 확장 없는 스트림
exl-id: ef81bfd2-2bfa-4ff7-b826-fd80802b3c07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 확장 없는 스트림{#extensionless-streams}

브라우저 TVSDK는 현재 매니페스트 및 조각에 확장이 포함되지 않은 스트림 재생을 지원합니다.

## 조각 수준 {#section_0E035129501D4A77BBC14192D8A53A86}

브라우저 TVSDK는 응답의 처음 몇 바이트를 구문 분석하여 확장 없는 조각의 콘텐츠 유형을 감지합니다. 유효한 콘텐츠 유형이 검색되지 않으면 브라우저 TVSDK에서 오류가 발생합니다.

## 매니페스트 수준 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

브라우저 TVSDK는 `mediaResource.resourceType` 에 전달되는 매개 변수 `replaceCurrentResource` 매니페스트 URL의 콘텐츠 형식을 감지하는 방법입니다. 자세한 내용은 `AdobePSDK.MediaPlayer` 클래스.

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

If `resourceType` 이 제공되지 않으면 UI 프레임워크는 리소스 URL 확장에서 리소스 유형을 결정한 다음 로 전달합니다. `replaceCurrentResource` 메서드를 사용합니다.

>[!TIP]
>
>확장 없는 매니페스트의 경우 다음을 확인하십시오. `resourceType` 는 UI 프레임워크에서 리소스를 로드하는 동안 항상 전달됩니다.

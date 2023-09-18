---
description: 캡션 텍스트의 글꼴, 크기, 색상, 가장자리 및 불투명도와 같은 형식을 설정할 수 있습니다.
title: 선택 캡션 스타일 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 선택 캡션 스타일 설정{#set-closed-caption-styles}

캡션 텍스트의 글꼴, 크기, 색상, 가장자리 및 불투명도와 같은 형식을 설정할 수 있습니다.

1. 다음을 기다리십시오. `MediaPlayer` PREPARED 상태 이상이어야 합니다.

   상태에 대한 자세한 내용은 [유효한 상태를 기다립니다.](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. 만들기 `TextFormat` 인스턴스.

   모든 자막 스타일 매개 변수를 지금 제공하거나 나중에 설정할 수 있습니다.

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. (선택 사항) 다음을 사용하여 현재 자막 스타일 설정 가져오기 `MediaPlayer.ccStyle`.

   반환 값은 `TextFormat` 인터페이스.

   이전에 설정한 스타일이 없으면 각 속성에 대한 기본값이 있는 TextFormat 개체가 반환됩니다.

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 스타일 설정을 변경하려면 `MediaPlayer.ccStyle`, 의 인스턴스 전달 `TextFormat` 인터페이스.

   현재 미디어 스트림에 폐쇄 캡션이 없는 경우에도 이 방법을 사용할 수 있습니다.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >폐쇄 캡션 스타일을 설정하는 것은 비동기적이므로 변경 사항이 화면에 표시되는 데 몇 초 정도 걸릴 수 있습니다.

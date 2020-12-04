---
description: 자막 텍스트의 글꼴, 크기, 색상, 가장자리 및 불투명도와 같은 형식을 설정할 수 있습니다.
seo-description: 자막 텍스트의 글꼴, 크기, 색상, 가장자리 및 불투명도와 같은 형식을 설정할 수 있습니다.
seo-title: 자막 스타일 설정
title: 자막 스타일 설정
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# 닫힌 캡션 스타일 설정{#set-closed-caption-styles}

자막 텍스트의 글꼴, 크기, 색상, 가장자리 및 불투명도와 같은 형식을 설정할 수 있습니다.

1. `MediaPlayer`이(가) PREMITED 상태여야 합니다.

   상태에 대한 자세한 내용은 [유효한 상태](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)를 기다립니다.
1. `TextFormat` 인스턴스를 만듭니다.

   이제 모든 자막 스타일 지정 매개 변수를 제공하거나 나중에 설정할 수 있습니다.

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

1. (선택 사항) `MediaPlayer.ccStyle`으로 현재 자막 스타일 설정을 가져옵니다.

   반환 값은 `TextFormat` 인터페이스의 인스턴스입니다.

   이전에 설정된 스타일이 없으면 각 특성에 대한 기본값이 있는 TextFormat 객체를 반환합니다.

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 스타일 설정을 변경하려면 `MediaPlayer.ccStyle`을(를) 사용하여 `TextFormat` 인터페이스의 인스턴스를 전달합니다.

   현재 미디어 스트림에 자막이 없는 경우에도 이 방법을 사용할 수 있습니다.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >자막 스타일을 설정하는 것은 비동기 방식이므로 변경 사항이 화면에 나타나는 데 몇 초 정도 걸릴 수 있습니다.


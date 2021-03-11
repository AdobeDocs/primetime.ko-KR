---
description: 닫힌 캡션 텍스트의 글꼴, 크기, 색상, 가장자리 및 불투명도와 같은 형식을 설정할 수 있습니다.
title: 닫힌 캡션 스타일 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 닫힌 캡션 스타일 설정{#set-closed-caption-styles}

닫힌 캡션 텍스트의 글꼴, 크기, 색상, 가장자리 및 불투명도와 같은 형식을 설정할 수 있습니다.

1. `MediaPlayer`이(가) PREPARED 상태여야 합니다.

   상태에 대한 자세한 내용은 [유효한 상태](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)를 기다립니다.
1. `TextFormat` 인스턴스를 만듭니다.

   이제 모든 닫힌 캡션 스타일 지정 매개 변수를 제공하거나 나중에 설정할 수 있습니다.

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

1. (선택 사항) `MediaPlayer.ccStyle`으로 현재 닫힌 캡션 스타일 설정을 가져옵니다.

   반환 값은 `TextFormat` 인터페이스의 인스턴스입니다.

   이전에 설정된 스타일이 없으면 각 속성에 대한 기본값이 있는 TextFormat 객체를 반환합니다.

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 스타일 설정을 변경하려면 `MediaPlayer.ccStyle`을 사용하여 `TextFormat` 인터페이스의 인스턴스를 전달합니다.

   현재 미디어 스트림에 자막이 없는 경우에도 이 메서드를 사용할 수 있습니다.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >닫힌 캡션 스타일을 설정하는 것은 비동기적이므로 변경 내용이 화면에 나타나는 데 몇 초 정도 걸릴 수 있습니다.


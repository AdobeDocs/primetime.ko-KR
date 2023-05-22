---
description: 폐쇄 캡션 서식을 지정할 수 있습니다.
title: 예제 캡션 서식
exl-id: 946530a1-c7d7-4582-81b8-71b2980561cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '33'
ht-degree: 0%

---

# 예: 캡션 서식{#examples-caption-formatting}

폐쇄 캡션 서식을 지정할 수 있습니다.

## 예제 1: 형식 값을 명시적으로 지정 {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```js
// Set CC style. 
var tf = new AdobePSDK.TextFormat( 
      AdobePSDK.TextFormat.FONT_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.FONT_EDGE_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.SIZE_DEFAULT, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY; 
 mediaPlayer.CCStyle(tf);
```

>[!IMPORTANT]
>
>브라우저 TVSDK는 글꼴 에지, 채우기 색상 또는 채우기 불투명도를 지원하지 않습니다.

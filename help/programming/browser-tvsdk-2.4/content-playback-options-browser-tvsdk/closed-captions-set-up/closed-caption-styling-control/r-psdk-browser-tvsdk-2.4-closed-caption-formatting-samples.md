---
description: 닫힌 캡션 서식을 지정할 수 있습니다.
title: 예제 캡션 서식
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '33'
ht-degree: 0%

---


# 예:캡션 서식{#examples-caption-formatting}

닫힌 캡션 서식을 지정할 수 있습니다.

## 예 1:형식 값을 명시적으로 {#section_BD7B48F3B66D4E9290E1CB2F464E08E4} 지정합니다.

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
>브라우저 TVSDK는 글꼴 가장자리, 칠 색상 또는 칠 불투명도를 지원하지 않습니다.


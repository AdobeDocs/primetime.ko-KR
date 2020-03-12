---
description: 자막 서식을 지정할 수 있습니다.
seo-description: 자막 서식을 지정할 수 있습니다.
seo-title: 예제 캡션 서식
title: 예제 캡션 서식
uuid: d55a506a-6662-4252-95f6-4073b2997f3b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 예:캡션 서식{#examples-caption-formatting}

자막 서식을 지정할 수 있습니다.

## 예 1:명시적으로 형식 값 지정 {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

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


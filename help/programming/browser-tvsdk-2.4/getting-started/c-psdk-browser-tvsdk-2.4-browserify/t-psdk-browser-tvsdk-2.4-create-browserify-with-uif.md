---
description: 앱에서 Browser TVSDK에서 제공하는 Browserify 라이브러리 파일을 사용하여 UI 프레임워크를 사용하여 Browserialize와 호환되는 플레이어를 만듭니다.
title: UI 프레임워크를 사용하여 Browserialize 호환 플레이어 만들기
exl-id: cd72cae1-f67e-4192-9a7e-1c1492d88922
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# UI 프레임워크를 사용하여 Browserialize 호환 플레이어 만들기 {#create-a-browserify-compatible-player-using-the-ui-framework}

앱에서 Browser TVSDK에서 제공하는 Browserify 라이브러리 파일을 사용하여 UI 프레임워크를 사용하여 Browserialize와 호환되는 플레이어를 만듭니다.

TVSDK에 포함된 샘플 Browserialize 파일:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

UI 프레임워크를 사용하여 Browserialize 호환 앱을 만들려면 다음을 수행해야 합니다 `require` 앱 코드에서 두 개의 Browserialize 모듈(브라우저 TVSDK에서 제공됨)은

1. Browserialize 모듈 필요:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. 에 설명된 대로 개발을 진행하십시오. [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>이제 Browserify를 사용하여 앱 파일을 번들로 묶을 수 있습니다.

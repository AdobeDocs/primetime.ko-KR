---
description: UI-Framework를 사용하여 브라우저 TVSDK에서 제공하는 브라우저 라이브러리 파일을 사용하여 브라우저 호환 플레이어를 만듭니다.
title: UI-프레임워크를 사용하여 브라우저 호환 플레이어 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# UI-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}를 사용하여 브라우저 호환 플레이어를 만듭니다.

UI-Framework를 사용하여 브라우저 TVSDK에서 제공하는 브라우저 라이브러리 파일을 사용하여 브라우저 호환 플레이어를 만듭니다.

TVSDK에 포함된 샘플 브라우저 파일:

* [!DNL [..]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/ui-framework/build/package.json]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.js]

UI-Framework를 사용하여 브라우저 호환 앱을 만들려면 앱 코드에 브라우저 TVSDK에서 제공하는 2개의 브라우저 시리즈 모듈(Browser TVSDK에서 제공)을 `require`해야 합니다.

1. 브라우저 시리즈 모듈 필요:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md)에 설명된 대로 개발을 계속하십시오.
>이제 Browserify를 사용하여 앱 파일을 번들로 묶을 수 있습니다.

---
description: 앱에서 브라우저 TVSDK가 제공하는 브라우저 라이브러리 파일을 사용하여 UI-프레임워크를 사용하여 브라우저 호환 플레이어를 제작할 수 있습니다.
seo-description: 앱에서 브라우저 TVSDK가 제공하는 브라우저 라이브러리 파일을 사용하여 UI-프레임워크를 사용하여 브라우저 호환 플레이어를 제작할 수 있습니다.
seo-title: UI-프레임워크를 사용하여 브라우저 호환 플레이어 만들기
title: UI-프레임워크를 사용하여 브라우저 호환 플레이어 만들기
uuid: 544fd872-5ca1-417d-8aab-69613caada0e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# UI-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}을(를) 사용하여 Browserie 호환 플레이어를 만듭니다.

앱에서 브라우저 TVSDK가 제공하는 브라우저 라이브러리 파일을 사용하여 UI-프레임워크를 사용하여 브라우저 호환 플레이어를 제작할 수 있습니다.

TVSDK에 포함된 샘플 브라우저 파일:

* [!DNL [..]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/ui-framework/build/package.json]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.js]

UI-Framework를 사용하여 브라우저 호환 앱을 만들려면 앱 코드에 브라우저 TVSDK에서 제공하는 두 개의 브라우저 시리즈 모듈(`require`)을 제공해야 합니다.

1. 검색 모듈 필요:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md)에 설명된 대로 개발을 진행하십시오.
>이제 Browserify를 사용하여 앱 파일을 번들로 제공할 수 있습니다.

---
description: 앱에서 Browser TVSDK에서 제공한 Browserify 라이브러리 파일을 사용하여 Browserialize와 호환되는 플레이어를 만듭니다.
title: UI 프레임워크 없이 Browserialize와 호환되는 플레이어 만들기
exl-id: 27b5e1c5-49c3-44e4-9e34-0f50a50e36f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# UI 프레임워크 없이 Browserialize와 호환되는 플레이어 만들기{#create-a-browserify-compatible-player-without-the-ui-framework}

앱에서 Browser TVSDK에서 제공한 Browserify 라이브러리 파일을 사용하여 Browserialize와 호환되는 플레이어를 만듭니다.

주제 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) 기본 비디오 플레이어를 만들 때 일반적으로 포함하는 브라우저 TVSDK 라이브러리 세트를 나열합니다. 이렇게 하려면 다음을 추가하기만 하면 됩니다. `script` 태그 포함 `src` 라이브러리를 가리키는 속성입니다.

Browserialize 호환 플레이어를 만드는 프로세스는 약간 다릅니다. 이를 위해 다음을 사용합니다. `require` 포함할 명령 [!DNL AdobePSDK.module.js] 앱의 파일(브라우저 TVSDK에서 제공)입니다. 이 파일은 기본 플레이어 라이브러리 파일을 적절한 종속성 순서로 번들로 제공하고 `AdobePSDK` 플레이어의 기능을 구현하는 데 사용하는 네임스페이스입니다.

Browser TVSDK는 릴리스 패키지에서 다음 샘플 Browserialize 응용 프로그램 및 빌드 파일을 제공합니다.

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Browserialize와 호환되는 비디오 플레이어를 만들려면:

1. 를 반환하는 Browserify 호환 라이브러리 파일이 필요합니다. `AdobePSDK` 네임스페이스:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 에 설명된 대로 플레이어를 만듭니다. [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   이 작업의 1단계는 앱 파일에 개별 기본 플레이어 라이브러리를 소싱하는 기본 플레이어 지침의 단계를 대체합니다.
이제 Browserify를 사용하여 앱 파일을 번들로 묶을 수 있습니다.

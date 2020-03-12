---
description: Browser TVSDK가 앱에 제공하는 BrowserSerify 라이브러리 파일을 사용하여 브라우저 호환 플레이어를 만듭니다.
seo-description: Browser TVSDK가 앱에 제공하는 BrowserSerify 라이브러리 파일을 사용하여 브라우저 호환 플레이어를 만듭니다.
seo-title: UI-프레임워크 없이 브라우저 호환 플레이어 만들기
title: UI-프레임워크 없이 브라우저 호환 플레이어 만들기
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# UI-프레임워크 없이 브라우저 호환 플레이어 만들기{#create-a-browserify-compatible-player-without-the-ui-framework}

Browser TVSDK가 앱에 제공하는 BrowserSerify 라이브러리 파일을 사용하여 브라우저 호환 플레이어를 만듭니다.

이 항목에서는 기본 비디오 플레이어를 만들 때 일반적으로 포함하는 브라우저 TVSDK 라이브러리 세트를 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) 나열합니다. 이렇게 하려면 라이브러리를 가리키는 `script` 특성이 있는 `src` 태그를 추가하면 됩니다.

브라우저 호환 플레이어를 만드는 프로세스는 약간 다릅니다. 이를 위해 `require` 명령을 사용하여 [!DNL AdobePSDK.module.js] 파일(브라우저 TVSDK에서 제공)을 앱에 포함합니다. 이 파일은 기본 플레이어 라이브러리 파일을 적절한 순서대로 번들하고 플레이어에 대한 기능을 구현하는 데 사용하는 `AdobePSDK` 네임스페이스를 반환합니다.

Browser TVSDK는 릴리스 패키지에서 다음과 같은 샘플 Browser Application 및 빌드 파일을 제공합니다.

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

브라우저 호환 비디오 플레이어를 만들려면:

1. 네임스페이스를 반환하는 Browserie-compatible 라이브러리 파일이 `AdobePSDK` 필요합니다.

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 에 설명된 대로 플레이어를 만듭니다 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   이 작업의 1단계는 앱 파일에서 개별 기본 플레이어 라이브러리를 소스로 하는 기본 플레이어 지침의 단계를 대체합니다.
이제 Browserify를 사용하여 앱 파일을 번들로 제공할 수 있습니다.

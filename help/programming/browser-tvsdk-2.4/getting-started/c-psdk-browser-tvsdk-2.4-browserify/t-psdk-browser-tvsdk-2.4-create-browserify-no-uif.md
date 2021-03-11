---
description: 브라우저 TVSDK에서 제공하는 브라우저 라이브러리 파일을 앱에서 사용하여 브라우저 호환 플레이어를 만듭니다.
title: UI-프레임워크 없이 브라우저 호환 플레이어 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework} 없이 브라우저 호환 플레이어를 만듭니다.

브라우저 TVSDK에서 제공하는 브라우저 라이브러리 파일을 앱에서 사용하여 브라우저 호환 플레이어를 만듭니다.

[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) 항목에는 기본 비디오 플레이어를 만들 때 일반적으로 포함하는 브라우저 TVSDK 라이브러리 집합이 나열됩니다. 라이브러리를 가리키는 `src` 특성이 있는 `script` 태그를 추가하면 됩니다.

브라우저 호환 플레이어를 만드는 프로세스는 약간 다릅니다. 이를 위해 `require` 명령을 사용하여 [!DNL AdobePSDK.module.js] 파일(브라우저 TVSDK에서 제공)을 앱에 포함합니다. 이 파일은 기본 플레이어 라이브러리 파일을 올바른 순서로 번들하고 플레이어에 대한 기능을 구현하는 데 사용하는 `AdobePSDK` 네임스페이스를 반환합니다.

Browser TVSDK는 릴리스 패키지에서 다음과 같은 샘플 Browserify 애플리케이션 및 빌드 파일을 제공합니다.

* [!DNL [..]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/reference/build/package.json]
* [!DNL [..]/samples/browserify/reference/examples/sample.html]
* [!DNL [..]/samples/browserify/reference/examples/sample.js]

브라우저 호환 비디오 플레이어를 만들려면 다음을 수행하십시오.

1. `AdobePSDK` 네임스페이스를 반환하는 Browserify 호환 라이브러리 파일이 필요합니다.

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)에 설명된 대로 플레이어를 만듭니다.

   이 작업의 1단계는 앱 파일에 있는 개별 기본 플레이어 라이브러리를 소스를 생성하는 기본 플레이어 지침의 단계를 대체합니다.
이제 Browserify를 사용하여 앱 파일을 번들로 묶을 수 있습니다.

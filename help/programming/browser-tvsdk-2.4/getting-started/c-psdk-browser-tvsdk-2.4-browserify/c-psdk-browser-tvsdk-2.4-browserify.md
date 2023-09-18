---
description: 브라우저 TVSDK에서 제공하는 JS 파일을 사용하여 Browserialize 호환 플레이어를 만들 수 있습니다.
title: Browserify 호환 플레이어
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 개요 {#browserify-compatible-player-overview}

브라우저 TVSDK에서 제공하는 JS 파일을 사용하여 Browserialize 호환 플레이어를 만들 수 있습니다.

브라우저 TVSDK는 Browserialize와 호환되는 JS 파일 두 개를 제공합니다. 하나는 AdobePSDK 모듈과 함께 사용하기 위한 것으로서, UI 프레임워크 없이 앱을 개발하기 위한 것입니다. 다른 하나는 UI 프레임워크 모듈과 함께 사용하기 위한 것입니다. UI 프레임워크를 사용하여 앱을 작성하는 데 사용하는 PTP 네임스페이스를 반환합니다.

Browserify를 시작하려면 다음 설치 명령을 실행하여 [!DNL final.js] 파일(Browserify 번들 파일) [!DNL example] 아래의 디렉터리 [!DNL samples/browerify/reference] 및 [!DNL samples/browerify/ui-framework]:

1. 다음으로 이동 [!DNL samples/browserify/reference/build].
1. 다음 명령을 실행합니다.

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 다음으로 이동 [!DNL samples/browserify/ui-framework/build].
1. 2단계와 동일한 명령을 실행합니다.

이 설정이 완료되면 TVSDK와 함께 제공된 샘플을 기반으로 하여 Browserialize 호환 TVSDK 앱을 계속 만들 수 있습니다.

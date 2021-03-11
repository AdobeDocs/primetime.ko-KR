---
description: 브라우저 TVSDK에서 제공하는 JS 파일을 사용하여 브라우저 호환 플레이어를 만들 수 있습니다.
title: 브라우저 호환 플레이어
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 개요 {#browserify-compatible-player-overview}

브라우저 TVSDK에서 제공하는 JS 파일을 사용하여 브라우저 호환 플레이어를 만들 수 있습니다.

브라우저 TVSDK는 두 개의 브라우저 호환 JS 파일을 제공합니다. 하나는 AdobePSDK 모듈과 함께 사용하는 것입니다.UI-Framework 없이 앱을 개발할 수 있습니다. 다른 하나는 UI-Framework 모듈과 함께 사용하는 것입니다.UI-Framework를 사용하여 앱을 작성하는 데 사용하는 PTP 네임스페이스를 반환합니다.

Browserify를 시작하려면 다음 설정 명령을 실행하여 [!DNL samples/browerify/reference] 및 [!DNL samples/browerify/ui-framework] 아래의 [!DNL example] 디렉토리 내에 [!DNL final.js] 파일(Browsertify 번들 파일)을 만듭니다.

1. [!DNL samples/browserify/reference/build]으로 이동합니다.
1. 다음 명령을 실행합니다.

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. [!DNL samples/browserify/ui-framework/build]으로 이동합니다.
1. 2단계에서와 동일한 명령을 실행합니다.

이 설정이 완료되면 TVSDK와 함께 제공된 샘플을 기반으로 브라우저 호환 TVSDK 앱을 계속 만들 수 있습니다.

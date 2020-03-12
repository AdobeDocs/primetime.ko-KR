---
description: 브라우저 TVSDK에서 제공하는 JS 파일을 사용하여 브라우저 호환 플레이어를 만들 수 있습니다.
seo-description: 브라우저 TVSDK에서 제공하는 JS 파일을 사용하여 브라우저 호환 플레이어를 만들 수 있습니다.
seo-title: 브라우저 호환 플레이어
title: 브라우저 호환 플레이어
uuid: 1832c826-d5d0-41b0-852f-286c8e4fa0f3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 개요 {#browserify-compatible-player-overview}

브라우저 TVSDK에서 제공하는 JS 파일을 사용하여 브라우저 호환 플레이어를 만들 수 있습니다.

브라우저 TVSDK는 두 개의 브라우저 호환 JS 파일을 제공합니다. 하나는 AdobePSDK 모듈과 함께 사용하는 것입니다.UI-Framework 없이 앱을 개발할 수 있습니다. 다른 하나는 UI-Framework 모듈과 함께 사용하는 것입니다.ui-Framework를 사용하여 앱을 작성하는 데 사용하는 PTP 네임스페이스를 반환합니다.

Browserify를 시작하려면 다음 설정 명령을 실행하여 [!DNL final.js] 파일(Browsertify bundle 파일)을 [!DNL example] 및 [!DNL samples/browerify/reference] [!DNL samples/browerify/ui-framework]의 디렉토리 내에 만듭니다.

1. 로 [!DNL samples/browserify/reference/build]이동합니다.
1. 다음 명령을 실행합니다.

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 로 [!DNL samples/browserify/ui-framework/build]이동합니다.
1. 2단계에서와 동일한 명령을 실행합니다.

이 설정이 완료되면 TVSDK와 함께 제공된 샘플을 기반으로 브라우저 호환 TVSDK 앱을 계속 만들 수 있습니다.

---
keywords: setSecure;VideoEngineView
title: 화면 캡처 사용
description: 화면 캡처 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# 화면 캡처 사용{#enable-screen-capture}

TVSDK는 기본적으로 화면 캡처를 허용하지 않습니다. 구성 시 플레이어는 `com.adobe.ave.VideoEngineView` 개체에서 `setSecure(true)`을 호출합니다. `VideoEngineView` 개체를 만들고 `VideoEngine` 개체에 제공해야 하므로 이 개체에 액세스할 수 있습니다.

앱에서 화면 캡처를 활성화하려면:

1. `com.adobe.ave.VideoEngineView` 개체를 구성합니다.
1. `VideoEngineView` 개체에서 `setSecure(false)`을(를) 호출합니다.

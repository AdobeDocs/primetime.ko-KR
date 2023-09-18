---
keywords: setSecure;VideoEngineView
title: 화면 캡처 활성화
description: 화면 캡처 활성화
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 화면 캡처 활성화{#enable-screen-capture}

TVSDK는 기본적으로 화면 캡처를 허용하지 않습니다. 플레이어가 호출함 `setSecure(true)` 다음에 있음 `com.adobe.ave.VideoEngineView` 공사 중인 객체. 을(를) 구성해야 하므로 이 개체에 액세스할 수 있습니다. `VideoEngineView` 개체를 만들고 `VideoEngine` 개체.

앱에서 화면 캡처를 활성화하려면:

1. 구성 `com.adobe.ave.VideoEngineView` 개체.
1. 호출 `setSecure(false)` 다음에 대한 `VideoEngineView` 개체.

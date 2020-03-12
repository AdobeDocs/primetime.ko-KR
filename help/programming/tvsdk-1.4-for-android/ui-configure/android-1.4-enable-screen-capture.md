---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: 화면 캡처 사용
title: 화면 캡처 사용
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 화면 캡처 사용{#enable-screen-capture}

TVSDK는 기본적으로 화면 캡처를 허용하지 않습니다. 선수가 공사 `setSecure(true)` 시간에 `com.adobe.ave.VideoEngineView` 목표를 호출한다. 객체를 만들어 객체에 제공해야 하므로 이 객체에 액세스할 수 `VideoEngineView` `VideoEngine` 있습니다.

앱에서 화면 캡처를 활성화하려면:

1. 개체를 `com.adobe.ave.VideoEngineView` 구성합니다.
1. 개체 `setSecure(false)` `VideoEngineView` 클릭.

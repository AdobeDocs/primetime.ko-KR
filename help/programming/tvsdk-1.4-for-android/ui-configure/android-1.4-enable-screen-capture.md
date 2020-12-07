---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: 화면 캡처 사용
title: 화면 캡처 사용
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# 화면 캡처 사용{#enable-screen-capture}

TVSDK는 기본적으로 화면 캡처를 허용하지 않습니다. 구성 시 플레이어는 `com.adobe.ave.VideoEngineView` 개체에서 `setSecure(true)`을 호출합니다. `VideoEngineView` 개체를 만들고 `VideoEngine` 개체에 제공해야 하므로 이 개체에 액세스할 수 있습니다.

앱에서 화면 캡처를 활성화하려면:

1. `com.adobe.ave.VideoEngineView` 개체를 구성합니다.
1. `VideoEngineView` 개체에서 `setSecure(false)`을(를) 호출합니다.

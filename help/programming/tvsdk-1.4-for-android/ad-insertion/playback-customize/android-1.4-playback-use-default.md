---
description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-title: 기본 재생 동작 사용
title: 기본 재생 동작 사용
uuid: ccda5223-17c1-4cda-b875-e706f5dc8648
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---


# 기본 재생 동작 사용 {#use-the-default-playback-behavior}

기본 광고 동작을 사용하도록 선택할 수 있습니다.

기본 동작을 사용하려면:

    * &#39;AdvertisingFactory&#39; 클래스를 구현하는 경우 &#39;createAdPolicySelector&#39;에 대해 null을 반환합니다.
    
    * &#39;AdvertisingFactory&#39; 클래스에 대한 사용자 지정 구현이 없는 경우 TVSDK는 기본 광고 정책 선택기를 사용합니다.
---
description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
title: 기본 재생 동작 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# 기본 재생 동작 사용 {#use-the-default-playback-behavior}

기본 광고 동작을 사용하도록 선택할 수 있습니다.

기본 비헤이비어를 사용하려면:

    * &#39;AdvertisingFactory&#39; 클래스를 구현하는 경우 &#39;createAdPolicySelector&#39;에 대해 null을 반환합니다.
    
    * &#39;AdvertisingFactory&#39; 클래스에 대한 사용자 정의 구현이 없는 경우 TVSDK는 기본 광고 정책 선택기를 사용합니다.
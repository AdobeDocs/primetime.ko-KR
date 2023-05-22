---
description: 기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.
title: 기본 재생 동작 사용
exl-id: c277db2a-546e-4097-96ce-83914b726576
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# 기본 재생 동작 사용 {#use-the-default-playback-behavior}

기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.

기본 비헤이비어를 사용하려면

    * 나만의 &#39;AdvertisingFactory&#39; 클래스를 구현하는 경우 &#39;createAdPolicySelector&#39;에 대해 null을 반환합니다.
    
    * &#39;AdvertisingFactory&#39; 클래스에 대한 사용자 지정 구현이 없는 경우 TVSDK는 기본 광고 정책 선택기 를 사용합니다.

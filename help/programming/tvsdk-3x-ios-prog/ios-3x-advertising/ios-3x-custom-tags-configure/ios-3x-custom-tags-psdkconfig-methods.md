---
description: PTSDKConfig 클래스를 사용하여 TVSDK에서 전체적으로 사용자 지정 태그 이름을 구성할 수 있습니다.
title: 태그에 대한 클래스 메서드 구성
exl-id: 017b766e-a6aa-4c14-af9a-2c88746e22c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 태그에 대한 클래스 메서드 구성 {#config-class-methods-for-tags}

PTSDKConfig 클래스를 사용하여 TVSDK에서 전체적으로 사용자 지정 태그 이름을 구성할 수 있습니다.

TVSDK는 스트림별 구성을 지정하지 않는 모든 미디어 스트림에 전역 구성을 자동으로 적용합니다.

`PTSDKConfig` 은 다음 메서드를 노출하여 사용자 지정 태그를 관리합니다.

| **특정 사용자 정의 태그 구독** |  |
|---|---|
| `subscribedTags` | 구독한 태그의 현재 목록을 검색합니다. |
| `setSubscribedTags` | 애플리케이션에 노출될 구독한 태그 목록을 설정합니다. |
| **기본 영업 기회 감지기에 사용되는 광고 태그 사용자 지정** |
| `adTags` | 현재 광고 태그 목록을 검색합니다. |
| `setAdTags` | 기본 영업 기회 생성기에 사용될 광고 태그 목록을 설정합니다. |


다음 사항을 기억하십시오.

* setter 메서드는 태그 매개 변수에 null 값을 포함할 수 없습니다.
* 사용자 지정 태그 이름에는 # 접두사가 있어야 합니다.

   예를 들어 #EXT-X-ASSET은 올바른 사용자 지정 태그 이름이지만 EXT-X-ASSET은 올바르지 않습니다.
* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.

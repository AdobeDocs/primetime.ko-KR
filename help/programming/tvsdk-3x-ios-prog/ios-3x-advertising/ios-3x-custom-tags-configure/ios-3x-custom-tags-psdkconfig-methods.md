---
description: PTSDKConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-description: PTSDKConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-title: 태그에 대한 구성 클래스 메서드
title: 태그에 대한 구성 클래스 메서드
uuid: 27f1df0a-bbd3-4d80-820e-b659f2f33069
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# {#config-class-methods-for-tags} 태그에 대한 구성 클래스 메서드

PTSDKConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.

TVSDK는 스트림별 구성을 지정하지 않는 모든 미디어 스트림에 전역 구성을 자동으로 적용합니다.

`PTSDKConfig` 사용자 지정 태그를 관리하기 위해 다음 메서드를 노출합니다.

| **특정 사용자 지정 태그 구독** |  |
|---|---|
| `subscribedTags` | 가입된 태그의 현재 목록을 검색합니다. |
| `setSubscribedTags` | 애플리케이션에 노출될 구독 태그 목록을 설정합니다. |
| **기본 기회 탐지에 사용되는 광고 태그 사용자 정의** |
| `adTags` | 광고 태그의 현재 목록을 검색합니다. |
| `setAdTags` | 기본 기회 생성기에서 사용할 광고 태그 목록을 설정합니다. |


다음 사항을 기억하십시오.

* setter 메서드에서는 태그 매개 변수에 null 값을 포함할 수 없습니다.
* 사용자 지정 태그 이름에는 # 접두사가 포함되어야 합니다.

   예를 들어, #EXT-X-ASSET은 올바른 사용자 지정 태그 이름이지만 EXT-X-ASSET이 잘못되었습니다.
* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.
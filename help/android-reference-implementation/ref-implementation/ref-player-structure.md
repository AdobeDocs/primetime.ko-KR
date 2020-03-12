---
description: 이 기능 관리자는 TVSDK 라이브러리 주변에서 랩퍼 역할을 합니다.
seo-description: 이 기능 관리자는 TVSDK 라이브러리 주변에서 랩퍼 역할을 합니다.
seo-title: 참조 구현 구조
title: 참조 구현 구조
uuid: ae347a97-1500-476a-9fc8-c99e6b2ab8de
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 참조 구현 구조 {#reference-implementation-structure}

이 기능 관리자는 TVSDK 라이브러리 주변에서 랩퍼 역할을 합니다.

Java에서 클래스는 계층 구조로 구성됩니다. 예를 들어 아래의 모든 UI 관련 코드와 `com.adobe.primetime.reference.ui` 모든 기능 관리자는 아래에 `com.adobe.primetime.reference.manager`있습니다.

Primetime 참조 구현에는 다음 패키지가 포함되어 있습니다.

| 패키지 | 설명 |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | 이 클래스는 android.app.Application을 확장합니다. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | 사용자 지정 광고에 대한 코드를 포함합니다. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | 기능 관리자를 구성하는 데 필요한 인터페이스 코드를 포함합니다. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | DRM에 대한 도우미 클래스를 포함합니다. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | 인터페이스, 플랫폼 및 참조 정보를 위한 어댑터 및 항목 어댑터 FeedAdapterFactory, ContentRenditionInfo 및 XMLParserHelper 코드도 포함되어 있습니다. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | 로컬 및 원격 로깅을 위한 클래스를 제공합니다. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | 여기에서 ManagerFactory뿐만 아니라 기능 관리자를 찾을 수 있습니다. 활성화 또는 비활성화할 수 있는 선택적 기능의 경우 두 가지 기능 관리자가 있습니다. <ul><li>기능 이름인 기능 관리자(예: CCManager) 이 기능 관리자는 비활성화되어 있으며 기본 해제 동작을 제공합니다.</li><li>기능 관리자 이름에 켜기가 추가된 기능 관리자(예: CCManagerOn) 이 기능 관리자는 활성화된 기능에 대한 샘플 코드를 제공합니다.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | 카탈로그에 대한 UI 코드를 포함합니다. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | 로그에 대한 UI 코드를 포함합니다. |
| [com.adobe.primetime.reference.ui.pllayer](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | 플레이어에 대한 UI 코드를 포함합니다. |
| [com.adobe.primetime.reference.ui.setsettings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | 설정에 대한 UI 코드를 포함합니다. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | 일반 유틸리티 클래스를 포함합니다. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | 유틸리티 클래스를 `HTTP-specific` 포함합니다. |

---
description: 광고 확인자가 작동하도록 하려면, 광고 결정 등의 광고 제공자는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.
seo-description: 광고 확인자가 작동하도록 하려면, 광고 결정 등의 광고 제공자는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.
seo-title: 광고 삽입 메타데이터
title: 광고 삽입 메타데이터
uuid: f40ed53b-eba1-4f70-a29c-90cac51e8a9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 개요 {#ad-insertion-metadata}

광고 확인자가 작동하도록 하려면, 광고 결정 등의 광고 제공자는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.

TVSDK에는 Primetime 광고 결정 라이브러리가 포함되어 있습니다. 컨텐츠가 Primetime 광고 결정 서버의 광고를 포함하려면 다음 필수 `AuditudeSettings` 정보를 제공해야 합니다.

* `mediaID`가 아닌 경우 비디오를 재생할 고유한 식별자입니다.

   발행자는 비디오 컨텐츠 및 광고 정보를 Adobe Primetime 광고 결정 서버에 제출할 때 `mediaID`을 할당합니다. 이 ID는 Primetime 광고 결정 기능이 서버에서 비디오에 대한 관련 광고 정보를 검색하는 데 사용됩니다.

* (선택 사항) `defaultMediaId`. 다음 조건이 충족될 때 제공되는 광고를 지정합니다.

   * 광고 서버에 대한 요청이 잘못되었거나 컨텐츠가 잘못 구성되었습니다.
   * Primetime 광고 결정 시 데이터 전달이 지연됩니다.
   * Primetime 광고 결정 백엔드 프로세스가 작동하지 않거나 작동하지 않습니다.

   >[!TIP]
   >
   >Adobe은 `defaultMediaId`을 사용하는 것이 좋습니다.

* Adobe에 의해 할당된 `zoneID`은 귀사 또는 웹 사이트를 식별합니다.
* 할당된 광고 서버의 도메인.
* 기타 타깃팅 매개 변수.

   광고 공급자의 요구 사항과 요구 사항에 따라 이러한 매개 변수를 포함할 수 있습니다.
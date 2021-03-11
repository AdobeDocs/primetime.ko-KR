---
description: 광고 확인자가 작동하도록 허용하려면, Adobe Primetime 광고 결정 등의 광고 제공자는 공급자에 대한 연결을 활성화할 수 있도록 구성 값이 필요합니다.
title: 광고 삽입 메타데이터
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 개요 {#ad-insertion-metadata-overview}

광고 확인자가 작동하도록 허용하려면, Adobe Primetime 광고 결정 등의 광고 제공자는 공급자에 대한 연결을 활성화할 수 있도록 구성 값이 필요합니다.

브라우저 TVSDK에는 Adobe Primetime 광고 결정 라이브러리가 포함되어 있습니다. 컨텐츠가 Adobe Primetime 광고 결정 서버의 광고를 포함하려면 응용 프로그램에서 다음과 같은 필수 AuditionSettings 정보를 제공해야 합니다.

* `mediaID`를 반환합니다. 이것은 재생할 비디오에 대한 고유 식별자입니다.

   발행자는 비디오 컨텐츠 및 광고 정보를 Adobe Primetime 광고 결정 서버에 제출할 때 mediaID를 할당합니다. 이 ID는 Adobe Primetime 광고 결정 기능이 서버에서 비디오에 대한 관련 광고 정보를 검색하는 데 사용됩니다.

* (선택 사항) `defaultMediaId`. 다음 조건이 충족될 때 제공되는 광고를 지정합니다.

   * 광고 서버에 대한 요청이 잘못되었거나 컨텐츠가 잘못 구성되어 있습니다.
   * Adobe Primetime 광고 결정 시 데이터 전파가 지연됩니다.
   * Adobe Primetime 광고 결정 백엔드 프로세스 중 하나가 오작동을 일으키거나 사용할 수 없습니다.

   >[!TIP]
   >
   >Adobe은 `defaultMediaId`을 사용하는 것이 좋습니다.

* Adobe에 의해 할당된 `zoneID`은 귀사 또는 웹 사이트를 식별합니다.
* 할당된 광고 서버의 도메인.
* 기타 타깃팅 매개 변수.

   광고 공급자의 필요성과 요구에 따라 이러한 매개 변수를 포함할 수 있습니다.
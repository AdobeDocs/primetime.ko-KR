---
description: 광고 확인자가 작동하도록 허용하려면 Adobe Primetime 광고 결정 등의 광고 제공업체는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.
seo-description: 광고 확인자가 작동하도록 허용하려면 Adobe Primetime 광고 결정 등의 광고 제공업체는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.
seo-title: 광고 삽입 메타데이터
title: 광고 삽입 메타데이터
uuid: 676e81b9-4c2b-487e-bc68-74879ca2966b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 개요 {#ad-nsertion-metadata-overview}

광고 확인자가 작동하도록 허용하려면 Adobe Primetime 광고 결정 등의 광고 제공업체는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.

TVSDK에는 Primetime 광고 결정 라이브러리가 포함되어 있습니다. 콘텐츠가 Primetime 광고 결정 서버의 광고를 포함하려면 다음 필수 `AuditudeSettings` 정보를 응용 프로그램에 제공해야 합니다.

* `mediaID`에 표시되는 값은 재생할 비디오의 고유 식별자입니다.

   발행자는 비디오 컨텐츠 및 광고 정보를 Adobe Primetime 광고 결정 서버에 제출할 때 mediaID를 할당합니다. 이 ID는 Primetime 광고 결정 시 서버에서 비디오에 대한 관련 광고 정보를 검색하는 데 사용됩니다.

* (선택 사항) `defaultMediaId`다음 조건을 충족할 때 제공되는 광고를 지정합니다.

   * 광고 서버에 대한 요청이 잘못되었거나 컨텐츠가 잘못 구성되었습니다.
   * Primetime 광고 결정 시 데이터 전달이 지연됩니다.
   * Primetime 광고 결정 백엔드 프로세스가 제대로 작동하지 않거나 사용할 수 없습니다.
   >[!TIP]
   >
   >Adobe는 이 방법을 사용하는 것이 좋습니다 `defaultMediaId`.

* Adobe `zoneID`가 지정하는 사용자의 회사 또는 웹 사이트를 확인합니다.
* 할당된 광고 서버의 도메인.
* 기타 타깃팅 매개 변수.

   광고 공급자의 요구 사항과 요구 사항에 따라 이러한 매개 변수를 포함할 수 있습니다.
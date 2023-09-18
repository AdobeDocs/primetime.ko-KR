---
description: Ad Resolver가 작동할 수 있도록 하려면 Adobe Primetime ad decisioning과 같은 광고 공급자는 공급자에 대한 연결을 활성화하기 위한 구성 값이 필요합니다.
title: 광고 삽입 메타데이터
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 개요 {#ad-insertion-metadata}

Ad Resolver가 작동할 수 있도록 하려면 Adobe Primetime ad decisioning과 같은 광고 공급자는 공급자에 대한 연결을 활성화하기 위한 구성 값이 필요합니다.

TVSDK에는 Primetime ad decisioning 라이브러리가 포함됩니다. Primetime ad decisioning 서버의 광고를 포함하는 콘텐츠에 대해 애플리케이션이 다음 필수 사항을 제공해야 합니다 `AuditudeSettings` 정보:

* `mediaID`: 재생할 비디오의 고유 식별자입니다.

  게시자는 `mediaID` Adobe Primetime ad decisioning 서버에 비디오 콘텐츠 및 광고 정보를 제출할 때. 이 ID는 Primetime ad decisioning에서 서버에서 비디오에 대한 관련 광고 정보를 검색하는 데 사용됩니다.

* (선택 사항) `defaultMediaId`: 다음 조건이 충족될 때에 제공되는 광고를 지정합니다.

   * 광고 서버에 대한 요청이 잘못되었거나 콘텐츠가 잘못 구성되었습니다.
   * Primetime 광고 의사 결정에서 데이터 전파가 지연되고 있습니다.
   * Primetime ad decisioning 백엔드 프로세스 중 하나가 제대로 작동하지 않거나 사용할 수 없습니다.

  >[!TIP]
  >
  >Adobe은 다음을 권장합니다. `defaultMediaId`.

* 사용자 `zoneID`는 Adobe에 의해 할당되며 회사 또는 웹 사이트를 식별합니다.
* 할당된 광고 서버의 도메인입니다.
* 기타 타깃팅 매개 변수.

  필요에 따라 광고 공급자의 필요에 따라 이러한 매개 변수를 포함할 수 있습니다.

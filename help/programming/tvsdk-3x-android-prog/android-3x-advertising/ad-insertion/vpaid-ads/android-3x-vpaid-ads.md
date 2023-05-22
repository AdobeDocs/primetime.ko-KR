---
description: 비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID) 2.0에서는 비디오 광고를 재생할 수 있는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.
title: VPAID 2.0 광고 지원
exl-id: 8cc08999-6047-4bd0-a09f-8a2e28e09766
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 개요 {#vpaid-ad-support-overview}

비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID) 2.0에서는 비디오 광고를 재생할 수 있는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.

지원되는 기능은 다음과 같습니다.

* VPAID 사양의 버전 2.0

   자세한 내용은 다음을 참조하십시오. [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* 주문형 비디오(VOD) 콘텐츠가 포함된 선형 VPAID 광고
* JavaScript VPAID 광고

   VPAID 광고는 JavaScript 기반이어야 하며, 광고 응답은 VPAID 광고의 미디어 유형을 다음으로 식별해야 합니다. `application/javascript`.

다음 기능은 지원되지 않습니다.

* VPAID 사양의 버전 1.0
* 스킵퍼블 광고
* 오버레이 광고, 동적 컴패니언 광고, 최소화 가능한 광고, 축소 가능한 광고 및 확장 가능한 광고와 같은 비선형 광고
* VPAID 광고 미리 로드
* 라이브 콘텐츠의 VPAID 광고
* Flash VPAID 광고

## API

다음 API 요소는 VPAID 2.0 광고를 지원합니다.

* 다음 `getCustomAdView` 방법 `MediaPlayer` 반환: `CustomAdView` VPAID 광고를 렌더링하는 웹 보기를 나타내는 개체(참조) [API 참조](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` vpaid 로드 프로세스의 시간 제한을 설정합니다. 기본 시간 초과 값은 10초입니다.

VPAID 광고가 재생되는 동안:

* VPAID 광고는 플레이어 보기 위의 보기 컨테이너에 표시되므로 플레이어 보기에서 사용자의 탭에 의존하는 코드는 작동하지 않습니다.
* 호출 대상 `pause` 및 `play` 플레이어 인스턴스에서 일시 중지하고 VPAID 광고를 다시 시작합니다.

* VPAID 광고는 대화형일 수 있으므로 사전 정의된 기간이 없습니다.

   광고 서버 응답에 지정된 광고 기간 및 총 광고 브레이크 기간이 정확하지 않을 수 있습니다.

---
description: 비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-description: 비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-title: VPAID 2.0 광고 지원
title: VPAID 2.0 광고 지원
uuid: e45e91d2-2aef-4d69-ac80-228d23e8fd7b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# 개요 {#vpaid-ad-support-overview}

비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.

지원되는 기능은 다음과 같습니다.

* VPAID 사양 버전 2.0

   자세한 내용은 [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)을 참조하십시오.
* VOD(Video-On-Demand) 컨텐츠가 포함된 선형 VPAID 광고
* JavaScript VPAID 광고

   VPAID 광고는 JavaScript 기반이어야 하며 광고 응답에서 VPAID 광고의 미디어 유형을 `application/javascript`으로 식별해야 합니다.

다음 기능은 지원되지 않습니다.

* VPAID 사양 버전 1.0
* 스케이프 광고
* 오버레이 광고, 동적 컴패니언 광고, 최소화 가능한 광고, 축소 가능한 광고 및 확장 가능한 광고와 같은 비선형 광고
* VPAID 광고 사전 로드
* 라이브 콘텐츠의 VPAID 광고
* Flash VPAID 광고

## API

다음 API 요소는 VPAID 2.0 광고를 지원합니다.

* `MediaPlayer`의 `getCustomAdView` 메서드는 VPAID 광고를 렌더링하는 웹 보기를 나타내는 `CustomAdView` 개체를 반환합니다([API 참조](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html) 참조).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` VPAID 로드 프로세스의 시간 초과를 설정합니다. 기본 시간 초과 값은 10초입니다.

VPAID 광고가 재생되는 동안:

* VPAID 광고는 플레이어 보기 위의 보기 컨테이너에 표시되므로 플레이어 보기에서 사용자의 탭 사용에 의존하는 코드가 작동하지 않습니다.
* 플레이어 인스턴스에서 `pause` 및 `play` 호출을 일시 중지하고 VPAID 광고를 다시 시작합니다.

* 광고는 대화형일 수 있으므로 VPAID 광고에 사전 정의된 기간이 없습니다.

   광고 서버 응답에 지정된 광고 지속 시간과 총 광고 중단 기간이 정확하지 않을 수 있습니다.
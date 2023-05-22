---
description: 비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID) 2.0에서는 비디오 광고를 재생할 수 있는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.
title: VPAID 2.0 광고 지원
exl-id: ee3e0cd9-463e-4de9-a94f-292e968b6f08
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# VPAID 2.0 광고 지원 {#vpaid-ad-support}

비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID) 2.0에서는 비디오 광고를 재생할 수 있는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.

지원되는 기능은 다음과 같습니다.

* VPAID 사양의 버전 2.0

   자세한 내용은 다음을 참조하십시오. [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* 선형 VPAID 광고 온디맨드(VOD) 콘텐츠
* JavaScript VPAID 광고

   VPAID 광고는 JavaScript 기반이어야 하며, 광고 응답은 VPAID 광고의 미디어 유형을 다음으로 식별해야 합니다. `application/javascript`.

다음 기능은 지원되지 않습니다.

* VPAID 사양의 버전 1.0
* 스킵퍼블 광고
* 오버레이 광고, 동적 컴패니언 광고, 최소화 가능한 광고, 축소 가능한 광고 및 확장 가능한 광고와 같은 비선형 광고
* VPAID 광고 미리 로드
* 라이브 콘텐츠의 VPAID 광고
* Flash VPAID 광고

## API 변경 사항 {#section_D62F3E059C6C493592D34534B0BFC150}

API가 다음과 같이 변경되었습니다.

* A `getCustomAdView` 함수가에 추가되었습니다. `MediaPlayer` 및 은 VPAID 광고를 렌더링하는 웹 보기를 반환합니다.

   에 대한 자세한 내용은 `CustomAdView` 이 함수에서 반환되는 개체는 다음을 참조하십시오. [API 참조](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* A `CUSTOM_AD` 미디어 플레이어 인스턴스에서 이벤트를 발송합니다.

   응용 프로그램은 다음을 구현하여 이벤트 콜백을 등록할 수 있습니다 `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` vpaid 로드 프로세스에서 기본 시간 제한을 변경할 수 있습니다.

   기본 시간 초과 값은 10초입니다.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

VPAID 광고가 재생되는 동안:

* VPAID 광고가 플레이어 보기 위의 보기 컨테이너에 표시되므로 플레이어 보기에서 사용자의 탭에 의존하는 코드가 작동하지 않습니다.
* 기본 콘텐츠 플레이어가 일시 중지되었으며에 호출합니다. `pause` 및 `play` 플레이어 인스턴스에서는 VPAID 광고를 일시 중지하고 다시 시작하는 데 사용됩니다.

* VPAID 광고는 대화형일 수 있으므로 사전 정의된 기간이 없습니다.

   광고 서버 응답으로 정의된 광고 기간 및 총 광고 브레이크 기간이 정확하지 않을 수 있습니다.

## VPAID 2.0 통합 구현 {#implement-vpaid-integration}

VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가합니다.

VPAID 2.0 지원을 추가하려면:

1. 사용자 지정 광고 보기를 플레이어 인터페이스에 추가합니다.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 사용자 지정 광고 이벤트에 대한 리스너를 추가합니다.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

---
description: 비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-description: 비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-title: VPAID 2.0 광고 지원
title: VPAID 2.0 광고 지원
uuid: 7168a6e4-9c5e-4d3a-8710-867cf98e4445
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---


# VPAID 2.0 광고 지원 {#vpaid-ad-support}

비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.

지원되는 기능은 다음과 같습니다.

* VPAID 사양 버전 2.0

   자세한 내용은 [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)을 참조하십시오.
* VOD(Video-On-Demand) 컨텐츠의 선형 VPAID 광고
* JavaScript VPAID 광고

   VPAID 광고는 JavaScript 기반이어야 하며 광고 응답에서 VPAID 광고의 미디어 유형을 `application/javascript`으로 식별해야 합니다.

다음 기능은 지원되지 않습니다.

* VPAID 사양 버전 1.0
* 스케이프 광고
* 오버레이 광고, 동적 동반자 광고, 최소화 가능한 광고, 축소 가능한 광고, 확장 가능한 광고 등의 비선형 광고
* VPAID 광고 사전 로드
* 라이브 콘텐츠의 VPAID 광고
* Flash VPAID 광고

## API 변경 내용 {#section_D62F3E059C6C493592D34534B0BFC150}

API는 다음과 같이 변경되었습니다.

* `getCustomAdView` 함수가 `MediaPlayer`에 추가되었으며 VPAID 광고를 렌더링하는 웹 보기를 반환합니다.

   이 함수에서 반환되는 `CustomAdView` 개체에 대한 자세한 내용은 [API 참조](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html)를 참조하십시오.

* 미디어 플레이어 인스턴스에서 `CUSTOM_AD` 이벤트가 전달됩니다.

   응용 프로그램은 `CustomAdEventListener`을(를) 구현하여 이벤트 콜백을 등록할 수 있습니다.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` VPAID 로드 프로세스의 기본 시간 초과를 변경할 수 있습니다.

   기본 시간 초과 값은 10초입니다.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

VPAID 광고가 재생되는 동안:

* VPAID 광고는 플레이어 보기 위의 보기 컨테이너에 표시되므로 플레이어 보기에서 사용자의 탭 사용에 의존하는 코드가 작동하지 않습니다.
* 기본 컨텐츠 플레이어가 일시 중지되고 플레이어 인스턴스의 `pause` 및 `play` 호출이 VPAID 광고를 일시 중지하고 다시 시작하는 데 사용됩니다.

* 광고는 대화형일 수 있으므로 VPAID 광고에 사전 정의된 기간이 없습니다.

   광고 서버 응답으로 정의된 광고 지속 시간과 총 광고 중단 기간이 정확하지 않을 수 있습니다.

## VPAID 2.0 통합 구현 {#implement-vpaid-integration}

VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.

VPAID 2.0 지원을 추가하려면:

1. 플레이어 인터페이스에 사용자 지정 광고 보기를 추가합니다.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 사용자 지정 광고 이벤트에 대한 리스너를 추가합니다.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

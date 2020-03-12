---
description: 배너 광고를 표시하려면 배너 인스턴스를 만들고 TVSDK가 광고 관련 이벤트를 수신하도록 허용해야 합니다.
seo-description: 배너 광고를 표시하려면 배너 인스턴스를 만들고 TVSDK가 광고 관련 이벤트를 수신하도록 허용해야 합니다.
seo-title: 배너 광고 표시
title: 배너 광고 표시
uuid: 7246dfab-860f-4b55-9554-49738a483406
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 배너 광고 표시 {#display-banner-ads}

배너 광고를 표시하려면 배너 인스턴스를 만들고 TVSDK가 광고 관련 이벤트를 수신하도록 허용해야 합니다.

TVSDK는 이벤트를 통해 선형 광고와 연관된 컴패니언 배너 광고 목록을 제공합니다. `AdPlaybackEventListener.onAdBreakStart`

매니페스트는 다음과 같은 방법으로 컴패니언 배너 광고를 지정할 수 있습니다.

* HTML 코드 조각
* iFrame 페이지의 URL
* 정적 이미지 또는 Adobe Flash SWF 파일의 URL

각 컴패니언 광고에 대해 TVSDK는 애플리케이션에 사용할 수 있는 유형을 나타냅니다.

1. 다음을 수행하는 `AdPlaybackEventListener.onAdBreakStart` 이벤트에 대한 리스너를 추가합니다.

   * 배너 인스턴스의 기존 광고를 지웁니다.
   * Get the list of companion ads from `Ad.getCompanionAssets`.
   * 컴패니언 광고 목록이 비어 있지 않으면 배너 인스턴스 목록을 반복합니다.

      각 배너 인스턴스(an `AdAsset`)에는 폭, 높이, 리소스 유형(html, iframe 또는 static)과 같은 정보와 함께 사용 가능한 배너를 표시하는 데 필요한 데이터가 포함되어 있습니다.
   * 비디오 광고에 첨부된 부록 광고가 없는 경우 컴패니언 자산 목록에는 해당 비디오 광고에 대한 데이터가 포함되어 있지 않습니다.
   * 독립 실행형 디스플레이 광고를 표시하려면 스크립트에 논리를 추가하여 일반 DFP(발행자용 DoubleClick) 표시 광고 태그를 해당 배너 인스턴스에 실행합니다.
   * 배너를 적절한 위치에 표시하는 함수에 배너 정보를 보냅니다.

      일반적으로 이것은 `div`이며, 함수는 배너를 표시하는 `div ID` 데 를 사용합니다.


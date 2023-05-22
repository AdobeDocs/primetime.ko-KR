---
description: 라이브 스트림 광고 삽입의 경우, 광고 브레이크의 모든 광고가 완료될 때까지 재생되기 전에 광고 브레이크를 종료해야 할 수 있습니다.
title: 조기 광고 브레이크 반환 구현
exl-id: 38386ab7-0e3b-4628-84eb-470d585eb929
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# 조기 광고 브레이크 반환 구현 {#implement-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우, 광고 브레이크의 모든 광고가 완료될 때까지 재생되기 전에 광고 브레이크를 종료해야 할 수 있습니다.

예를 들어 특정 스포츠 이벤트에서 광고 브레이크 기간을 알 수 없는 경우에는 광고 브레이크가 시작됩니다. TVSDK는 기본 기간을 제공하지만, 휴식기가 완료되기 전에 게임이 다시 시작되는 경우 광고 브레이크를 종료해야 합니다. 또 다른 예는 라이브 스트림에서 광고 브레이크 중 긴급 신호입니다.

1. 스플라이스 아웃/인 광고 마커 구독( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, 및 `#EXT-X-CUE`).

   광고 마커를 밖으로/안으로 연결하는 방법에 대한 자세한 내용은 을 참조하십시오. [기회 생성기 및 콘텐츠 해결자](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. 사용자 지정 사용 `ContentFactory`.
1. 위치 `retrieveGenerators()`, 사용 `SpliceInPlacementOpportunityGenerator`.

   예:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   사용자 지정 사용에 대한 자세한 내용 `ContentFactory`의 1단계 를 참조하십시오. [사용자 정의 영업 기회 감지기 구현](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) .

1. 동일한 사용자 지정 `ContentFactory`, 구현 `retrieveResolvers` 및 포함 `AuditudeResolver` 및 `SpliceInCustomResolver`.

   예:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

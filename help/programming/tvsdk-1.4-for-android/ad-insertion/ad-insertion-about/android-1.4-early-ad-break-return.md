---
description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-title: 조기 광고 중단 반환 구현
title: 조기 광고 중단 반환 구현
uuid: 41b70ee1-290b-4732-899e-32b234ec1d9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 조기 광고 중단 반환 구현 {#implement-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.

예를 들어, 특정 스포츠 이벤트의 광고 중단 기간은 중단이 시작되기 전에 알려지지 않을 수 있습니다. TVSDK는 기본 지속 시간을 제공하지만, 중단이 끝나기 전에 게임이 재개되는 경우 광고 중단이 종료되어야 합니다. 또 다른 예로 라이브 스트림에서 광고 중단 중 긴급 신호가 있습니다.

1. 스플라이스 아웃/인 광고 마커( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`및 `#EXT-X-CUE`)를 구독합니다.

   광고 마커를 분할하는 방법에 대한 자세한 내용은 기회 생성기 [및 컨텐츠 해상도를 참조하십시오](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. 사용자 정의 `ContentFactory`사용
1. 에서 `retrieveGenerators()`를 `SpliceInPlacementOpportunityGenerator`사용합니다.

   예:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   사용자 정의 사용에 대한 자세한 `ContentFactory`내용은 사용자 지정 기회 [탐지 구현의 1단계를 참조하십시오](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) .

1. 동일한 사용자 정의에서 `ContentFactory`및 를 구현하고 포함시킵니다 `retrieveResolvers` `AuditudeResolver` `SpliceInCustomResolver`.

   예:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```


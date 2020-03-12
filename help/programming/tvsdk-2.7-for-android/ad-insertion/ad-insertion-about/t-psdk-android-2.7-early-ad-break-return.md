---
description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-title: 조기 광고 중단 반환 구현
title: 조기 광고 중단 반환 구현
uuid: c67f2158-5df4-458c-a27a-6329c5d26638
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 조기 광고 중단 반환 구현 {#implement-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.

예를 들어, 특정 스포츠 이벤트의 광고 중단 기간은 중단이 시작되기 전에 알려지지 않을 수 있습니다. TVSDK는 기본 지속 시간을 제공하지만, 중단이 끝나기 전에 게임이 재개되는 경우 광고 중단이 종료되어야 합니다. 또 다른 예로 라이브 스트림에서 광고 중단 중 긴급 신호가 있습니다.

1. 마커에서 `#EXT-X-CUE-OUT`스플라이스 `#EXT-X-CUE-IN`아웃/스플라이스(splice)인 등록 및 `#EXT-X-CUE`등록

   광고 마커를 분할하는 방법에 대한 자세한 내용은 기회 생성기 [및 컨텐츠 해상도를 참조하십시오](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

1. 사용자 정의 `ContentFactory`사용
1. 에서 `retrieveGenerators`를 `SpliceInPlacementOpportunityGenerator`사용합니다.

   예:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   사용자 지정 사용 방법에 대한 자세한 `ContentFactory`내용은 사용자 지정 기회 [생성자 구현의 1단계를 참조하십시오](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md).

1. 동일한 사용자 정의에서 `ContentFactory`및 를 구현하고 포함시킵니다 `retrieveResolvers` `AuditudeResolver` `SpliceInCustomResolver`.

   예:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```


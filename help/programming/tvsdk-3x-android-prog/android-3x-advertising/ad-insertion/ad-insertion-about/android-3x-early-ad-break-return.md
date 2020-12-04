---
description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-title: 조기 광고 중단 반환 구현
title: 조기 광고 중단 반환 구현
uuid: 0e77414e-86f5-4979-9caa-eaf2f39144a2
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 조기 광고 중단 반환 구현 {#implement-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.

예를 들어, 일부 스포츠 이벤트의 광고 중단 기간은 중단이 시작되기 전에 알 수 없을 수 있습니다. TVSDK는 기본 지속 시간을 제공하지만, 중단이 끝나기 전에 게임이 재개되는 경우 광고 중단이 종료되어야 합니다. 또 다른 예로 라이브 스트림에서 광고 중단 중 응급 신호가 있습니다.

1. 마커에서 스플릿 아웃/스플리스인 `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` 및 `#EXT-X-CUE`를 구독합니다.
광고 마커를 분할하는 방법에 대한 자세한 내용은 [기회 생성기 및 컨텐츠 해상도](../../ad-insertion/content-resolver/android-3x-content-resolver.md)를 참조하십시오.
1. 사용자 지정 `ContentFactory`을(를) 사용하십시오.
1. `retrieveGenerators`에서 `SpliceInPlacementOpportunityGenerator`을 사용합니다.

   예:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   사용자 지정 `ContentFactory` 사용에 대한 자세한 내용은 [사용자 지정 기회 생성자 구현](../../ad-insertion/content-resolver/android-3x-opp-detector-impl-android.md)의 1단계를 참조하십시오.

1. 동일한 사용자 지정 `ContentFactory`에서 `retrieveResolvers`을(를) 구현하고 `AuditudeResolver` 및 `SpliceInCustomResolver`을(를) 포함합니다.

   예:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

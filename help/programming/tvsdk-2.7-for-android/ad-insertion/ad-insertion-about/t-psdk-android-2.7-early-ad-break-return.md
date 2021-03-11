---
description: 라이브 스트림 광고 삽입의 경우, 중단에 있는 모든 광고가 완료되기 전에 광고 나누기를 종료해야 할 수 있습니다.
title: 조기 광고 중단 반환 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# 조기 광고 중단 반환 구현 {#implement-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우, 중단에 있는 모든 광고가 완료되기 전에 광고 나누기를 종료해야 할 수 있습니다.

예를 들어, 일부 스포츠 이벤트에서 광고 중단의 지속 시간을 알 수 없는 경우 중단이 시작되기 전에는 알 수 없습니다. TVSDK는 기본 지속 시간을 제공하지만 중단이 끝나기 전에 게임이 재개되는 경우 광고 중단이 종료되어야 합니다. 또 다른 예로 라이브 스트림에서 광고 중단 도중 비상 신호가 발생합니다.

1. 마커에서 스플릿 아웃/스플리스인 `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` 및 `#EXT-X-CUE`를 구독합니다.

   광고 마커를 분할하는 방법에 대한 자세한 내용은 [기회 생성기 및 컨텐츠 해상도](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md)를 참조하십시오.

1. 사용자 지정 `ContentFactory`을(를) 사용합니다.
1. `retrieveGenerators`에서 `SpliceInPlacementOpportunityGenerator`을 사용합니다.

   예:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   사용자 지정 `ContentFactory` 사용에 대한 자세한 내용은 [사용자 지정 기회 생성자 구현](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md)의 1단계를 참조하십시오.

1. 동일한 사용자 지정 `ContentFactory`에서 `retrieveResolvers`을(를) 구현하고 `AuditudeResolver` 및 `SpliceInCustomResolver`을(를) 포함합니다.

   예:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```


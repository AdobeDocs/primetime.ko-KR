---
description: 응용 프로그램은 적절한 시간에 적절한 TimedMetadata 개체를 사용해야 합니다.
seo-description: 응용 프로그램은 적절한 시간에 적절한 TimedMetadata 개체를 사용해야 합니다.
seo-title: 시간 메타데이터 개체가 전달되면 저장
title: 시간 메타데이터 개체가 전달되면 저장
uuid: 0e6d2a42-37a8-477e-b925-66bbc23445c1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 시간 메타데이터 개체가 전달되면 저장 {#store-timed-metadata-objects-as-they-are-dispatched}

응용 프로그램은 적절한 시간에 적절한 TimedMetadata 개체를 사용해야 합니다.

컨텐츠 구문 분석 중 재생 전에 발생하는 TVSDK는 구독 태그를 식별하고 애플리케이션에 이러한 태그에 대해 알립니다. 각 타임라인과 연결된 시간은 재생 타임라인의 현지 `TimedMetadata` 시간입니다.

애플리케이션은 다음 작업을 완료해야 합니다.

1. 현재 재생 시간을 추적할 수 있습니다.
1. 전달된 `TimedMetadata` 개체에 현재 재생 시간을 일치시킵니다.

1. 시작 시간이 현재 로컬 재생 시간과 `TimedMetadata` 같은 위치를 사용합니다.

   다음 예는 `TimedMetadata` 개체를 한 번에 저장하는 방법을 보여줍니다 `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList = new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```


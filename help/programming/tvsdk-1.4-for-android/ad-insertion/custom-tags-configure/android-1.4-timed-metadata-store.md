---
description: 응용 프로그램은 적절한 시간에 적절한 TimedMetadata 개체를 사용해야 합니다.
title: 전달될 때 시간 메타데이터 객체 저장
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# {#store-timed-metadata-objects-as-they-are-dispatched}이(가) 전달될 때 시간 지정된 메타데이터 객체를 저장합니다.

응용 프로그램은 적절한 시간에 적절한 TimedMetadata 개체를 사용해야 합니다.

컨텐츠 구문 분석 중 재생 전에 발생하는 TVSDK는 구독 태그를 식별하고 애플리케이션에 이러한 태그에 대해 알립니다. 각 `TimedMetadata`에 연결된 시간은 재생 타임라인의 로컬 시간입니다.

응용 프로그램은 다음 작업을 완료해야 합니다.

1. 현재 재생 시간을 추적할 수 있습니다.
1. 현재 재생 시간을 전달된 `TimedMetadata` 개체와 일치시킵니다.

1. 시작 시간이 현재 로컬 재생 시간과 같은 `TimedMetadata`을 사용합니다.

   다음 예제에서는 `ArrayList`에서 `TimedMetadata` 개체를 저장하는 방법을 보여 줍니다.

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


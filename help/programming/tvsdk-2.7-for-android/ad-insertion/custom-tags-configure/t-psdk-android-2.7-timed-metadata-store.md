---
description: 응용 프로그램은 적절한 시간에 적절한 TimedMetadata 개체를 사용해야 합니다.
title: 시간이 지정된 메타데이터 개체가 발송될 때 이를 저장합니다.
exl-id: da7ee636-f3ac-4aac-9ca0-7075b8c910f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 시간이 지정된 메타데이터 개체가 발송될 때 이를 저장합니다. {#store-timed-metadata-objects-as-they-are-dispatched}

응용 프로그램은 적절한 시간에 적절한 TimedMetadata 개체를 사용해야 합니다.

재생 전에 발생하는 컨텐츠 구문 분석 중에 TVSDK는 구독한 태그를 식별하고 애플리케이션에 이러한 태그에 대해 알립니다.

>[!TIP]
>
>각 시간과 관련된 시간 `TimedMetadata` 는 재생 타임라인의 현지 시간입니다.

시간 초과된 메타데이터 개체를 발송할 때 저장하려면 다음을 수행합니다.

1. 현재 재생 시간을 추적합니다.
1. 현재 재생 시간을 발송된 시간과 일치 `TimedMetadata` 개체.

1. 사용 `TimedMetadata` 여기서 시작 시간은 현재 로컬 재생 시간과 같습니다.

   다음 예제는 저장 방법을 보여 줍니다 `TimedMetadata` 의 오브젝트 `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

---
description: 자신만의 기회 탐지기를 구현할 수 있습니다.
title: 사용자 정의 기회 탐지기 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 사용자 지정 기회 탐지기 구현{#implement-a-custom-opportunity-detector}

자신만의 기회 탐지기를 구현할 수 있습니다.

* 기회 생성기가 현재 미디어 스트림과 연결된 `TimedMetadata` 개체를 기반으로 하는 경우 `SpliceOutOpportunityGenerator` 또는 `TimedMetadataOpportunityGenerator`를 확장해야 합니다.

* 영업 기회 생성기가 외부 서비스(예: CIS)에서 제공하는 대역외 데이터를 기반으로 하는 경우 `OpportunityGenerator`을(를) 확장해야 합니다.

1. 사용자 정의 기회 생성기 만들기

       사용자 지정 기회 생성기가 &#39;TimedMetadata&#39; 개체를 기반으로 하는 경우 &#39;TimedMetadataOpportunityGenerator&#39;를 확장하고 다음 메서드를 재정의합니다.
   
   * `doConfigure` - 이 방법은 미디어 플레이어 항목이 만들어진 후 호출되며 필요한 경우 초기 기회 세트를 생성할 수 있는 기회를 제공합니다.
   * `doProcess` - 이 메서드는 새로 시작될 때마다 호출됩니다(예: 재생 목록/매니페스트가 새로  `TimedMetadata` 고쳐질 때마다 실시간/선형 스트림의 경우).

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
   
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
   
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. 사용자 정의 기회 생성기를 사용하는 사용자 정의 컨텐츠 팩토리를 만듭니다.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
   
           return result; 
       } 
   }
   ```

1. 재생할 미디어 스트림에 대한 사용자 정의 컨텐츠 팩토리를 등록합니다.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```


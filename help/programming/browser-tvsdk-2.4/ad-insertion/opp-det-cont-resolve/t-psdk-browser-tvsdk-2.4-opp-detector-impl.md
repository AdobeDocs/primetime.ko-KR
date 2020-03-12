---
description: OpportunityGenerator 인터페이스를 확장하여 고유한 기회 생성기를 구현할 수 있습니다.
seo-description: OpportunityGenerator 인터페이스를 확장하여 고유한 기회 생성기를 구현할 수 있습니다.
seo-title: 사용자 정의 기회 생성기 구현
title: 사용자 정의 기회 생성기 구현
uuid: b80da2da-32d5-41f7-86ca-936d6f25b015
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 사용자 정의 기회 생성기 구현{#implement-a-custom-opportunity-generator}

OpportunityGenerator 인터페이스를 확장하여 고유한 기회 생성기를 구현할 수 있습니다.

1. 사용자 정의 기회 생성기 만들기

   예:

   ```js
   /** 
   * Class implementing AdobePSDK.OpportunityGenerator interface 
   */ 
   CustomOpportunityGenerator = function () { 
   }; 
   
   CustomOpportunityGenerator.prototype = { 
       constructor: CustomOpportunityGenerator, 
       configureCallbackFunc: function (item, client, mode, playhead, playbackRange) {  
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current AdobePSDK.MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadatas = item.timedMetadata; 
       }, 
       updateCallbackFunc: function (playhead, playbackRange) { 
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve (opportunity); 
       }, 
       … 
   }; 
   ```

1. 사용자 지정 기회 생성기를 사용하는 사용자 정의 컨텐츠 팩터리를 만듭니다.

   예:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
          constructor: CustomContentFactory, 
          retrieveOpportunityGeneratorsCallbackFunc: function (item) { 
               var result = []; 
               result.push (new CustomOpportunityGenerator()); 
               return result; 
       }, 
       … 
   }; 
   ```

1. 재생할 미디어 스트림에 대한 사용자 정의 콘텐츠 팩터리를 등록합니다.

   UI Framework 플레이어에서 다음과 같이 사용자 정의 콘텐츠 팩터리를 지정할 수 있습니다.

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
           mediaPlayerItemConfig: { 
                   advertisingFactory: advertisingFactory 
           }, 
               mediaResource: { 
                   resourceUrl:'Specify Resource Url' 
          } 
     } 
   }); 
   ```


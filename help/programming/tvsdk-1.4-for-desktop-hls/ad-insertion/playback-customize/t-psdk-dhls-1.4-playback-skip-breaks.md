---
description: 기본적으로 TVSDK는 사용자가 광고 휴가를 원하는 경우 광고 중단이 자동으로 수행됩니다. 이전 중단 완료에서 경과한 시간이 일정 시간 이내인 경우 광고 나누기를 건너뛸 동작을 사용자 정의할 수 있습니다.
seo-description: 기본적으로 TVSDK는 사용자가 광고 휴가를 원하는 경우 광고 중단이 자동으로 수행됩니다. 이전 중단 완료에서 경과한 시간이 일정 시간 이내인 경우 광고 나누기를 건너뛸 동작을 사용자 정의할 수 있습니다.
seo-title: 일정 기간 동안 광고 중단 건너뛰기
title: 일정 기간 동안 광고 중단 건너뛰기
uuid: 1a18d5fd-c957-481b-83ae-2129590c1678
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# 일정 기간 동안 광고 중단 건너뛰기{#skip-ad-breaks-for-a-period-of-time}

기본적으로 TVSDK는 사용자가 광고 휴가를 원하는 경우 광고 중단이 자동으로 수행됩니다. 이전 중단 완료에서 경과한 시간이 일정 시간 이내인 경우 광고 나누기를 건너뛸 동작을 사용자 정의할 수 있습니다.

>[!IMPORTANT]
>
>광고를 건너뛸 내부 검색이 있는 경우 재생 중에 약간의 일시 중지가 있을 수 있습니다.

사용자 지정된 광고 정책 선택기의 다음 예는 사용자가 광고 나누기를 본 후 다음 5분(월 시간)에 광고를 건너뜁니다.

1. 기본 광고 정책 선택기를 확장하여 기본 동작을 무시합니다.

   ```
   /** 
    * Custom ad policy selector. 
    */ 
   public class CustomAdPolicySelector extends DefaultAdPolicySelector { 
   
       /** 
        * Default constructor. 
        * 
        * @param item Associated media player item. 
        */ 
       public function CustomAdPolicySelector(item:MediaPlayerItem) { 
           super(item); 
   
           item.player.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED,  
                                        onAdBreakCompleted); 
       } 
   
       override public function selectPolicyForAdBreak(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForAdBreak(adPolicyInfo); 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       override public function selectAdBreaksToPlay(adPolicyInfo:AdPolicyInfo):Vector.<AdBreakTimelineItem> { 
           if (shouldPlayAds()) { 
               return super.selectAdBreaksToPlay(adPolicyInfo); 
           } 
   
           return new Vector.<AdBreakTimelineItem>(); 
       } 
   
       override public function selectPolicyForSeekIntoAd(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForSeekIntoAd(adPolicyInfo); 
           } 
   
           return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
       } 
   
       private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
           _lastAdBreakPlayedTime = new Date().valueOf(); 
       } 
   
       private function shouldPlayAds():Boolean { 
           var currentTime:Number = new Date().valueOf(); 
           return isNaN(_lastAdBreakPlayedTime) 
                   ||  (currentTime - _lastAdBreakPlayedTime > _minimumInterval); 
       } 
   
       private var _lastAdBreakPlayedTime:Number = NaN; 
       private var _minimumInterval:Number = 300000; // 5 minutes in milliseconds 
   }
   ```

1. 사용자 지정 선택기를 사용하는 새 광고 공장을 만듭니다.

   ```
   public class CustomAdPolicyContentFactory extends DefaultContentFactory { 
   
       private var _adPolicySelector:CustomAdPolicySelector; 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomAdPolicyContentFactory() { 
   
       } 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
       if (!_adPolicySelector) { 
           _adPolicySelector = new CustomAdPolicySelector(item); 
       } 
   
       return _adPolicySelector; 
       } 
   }
   ```

1. MediaPlayer에 사용할 새 광고 팩토리 클래스를 등록하십시오.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```


---
description: 기본적으로 TVSDK는 사용자가 광고 브레이크를 검색할 때 광고 브레이크를 강제로 재생합니다. 이전 브레이크 완료에서 경과된 시간이 특정 분 이내인 경우 광고 브레이크를 건너뛰도록 동작을 사용자 지정할 수 있습니다.
title: 일정 기간 동안 광고 브레이크 건너뛰기
exl-id: 7d5ee788-4a67-4c70-acc7-a950e6b2db8a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 일정 기간 동안 광고 브레이크 건너뛰기{#skip-ad-breaks-for-a-period-of-time}

기본적으로 TVSDK는 사용자가 광고 브레이크를 검색할 때 광고 브레이크를 강제로 재생합니다. 이전 브레이크 완료에서 경과된 시간이 특정 분 이내인 경우 광고 브레이크를 건너뛰도록 동작을 사용자 지정할 수 있습니다.

>[!IMPORTANT]
>
>광고를 건너뛰려는 내부 찾기가 있는 경우 재생이 약간 일시 중지될 수 있습니다.

사용자 지정된 광고 정책 선택기의 다음 예제는 사용자가 광고 브레이크를 시청한 후 5분(벽면 시계 시간) 안에 광고를 건너뜁니다.

1. 기본 광고 정책 선택기를 확장하여 기본 동작을 재정의합니다.

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

1. 사용자 지정 선택기를 사용하는 새 광고 팩토리를 만듭니다.

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

1. MediaPlayer에 사용할 새 광고 팩토리 클래스를 등록합니다.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

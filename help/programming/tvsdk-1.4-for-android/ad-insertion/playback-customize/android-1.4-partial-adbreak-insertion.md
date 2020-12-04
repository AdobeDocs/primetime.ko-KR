---
description: TV와 같은 경험을 통해 광고 중간에 라이브 스트림으로 참여할 수 있습니다.
seo-description: TV와 같은 경험을 통해 광고 중간에 라이브 스트림으로 참여할 수 있습니다.
seo-title: 부분 광고 분리 삽입
title: 부분 광고 분리 삽입
uuid: 296a9b6a-9e9f-4ca7-ab8a-c8cbc98fb9af
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 부분 광고 분리 삽입 {#partial-ad-break-insertion}

TV와 같은 경험을 통해 광고 중간에 라이브 스트림으로 참여할 수 있습니다.

부분 광고 중단 기능을 사용하면 TV와 같은 경험을 모방할 수 있습니다. 여기서 클라이언트가 중간 롤에서 라이브 스트림을 시작하면 해당 중간 롤에서 시작됩니다. TV채널로 전환해 TV를 방영하는 것과 비슷한 방식이다.

예를 들어 사용자가 90초 광고 중단(3개의 30초 광고)의 중간에 참여하는 경우, 두 번째 광고(즉, 광고 나누기로 40초 후)에 10초 동안 참여하는 경우, 다음이 발생합니다.

* 두 번째 광고는 나머지 기간(20초) 뒤에 세 번째 광고가 재생됩니다.
* 부분적으로 재생된 광고(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기만 실행됩니다.

이 동작은 기본적으로 활성화되어 있지 않습니다. 앱에서 이 기능을 사용하려면 다음을 수행하십시오.

1. AdvertisingMetadata 클래스의 메서드 setEnableLivePreroll을 사용하여 라이브 프리롤을 비활성화합니다.

   ```
   advertisingMetadata.setEnableLivePreroll(String.valueOf(false))
   ```

1. 부분 광고 삽입 환경 설정을 켜십시오. MediaPlayer 인터페이스의 새로운 메서드 setPartialAdBreakPref를 사용하여 이 기능을 ON으로 전환합니다. getPartialAdBreakPref 메서드를 사용하여 이 기본 설정의 현재 상태를 찾습니다.

   ```
   MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
   
          mediaPlayer.setPartialAdBreakPref(true); 
   ```

1. 이 기능을 사용하려면 동작을 사용자 정의하려면 사용자 지정 광고 정책 선택기를 구현해야 합니다. 아직 AdvertisingFactory 클래스의 사용자 지정 구현이 없는 경우 새 AdvertisingFactory 구현을 추가합니다. createAdPolicySelector 메서드를 재정의합니다. 이 메서드는 AdPolicySelector 구현의 새 인스턴스를 반환합니다.

   아래 샘플 구현은 참조용으로 제공됩니다. 다음 샘플 구현은 com.adobe.mediacore 패키지에서 사용할 수 있습니다. 그러나 쉽게 참조할 수 있도록 단순화되며 그대로 사용하지 않는 것이 좋습니다.

   1. 샘플 광고 정책 선택기

      ```
       package com.adobe.mediacore;
      
      import com.adobe.mediacore.logging.Log; 
      import com.adobe.mediacore.logging.Logger; 
      import com.adobe.mediacore.metadata.*; 
      import com.adobe.mediacore.timeline.advertising.*; 
      
      import java.util.ArrayList; 
      import java.util.List; 
      
      public class PartialAdBreakAdPolicySelector implements AdPolicySelector { 
          private static final String LOG_TAG = "[PSDK]::" + DefaultAdPolicySelector.class.getSimpleName(); 
          private final Logger _logger = Log.getLogger(LOG_TAG); 
      
          private final MediaPlayerItem _mediaPlayerItem; 
          private final AdBreakAsWatched _adBreakAsWatchedPolicy; 
      
          public PartialAdBreakAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
              _mediaPlayerItem = mediaPlayerItem; 
              _adBreakAsWatchedPolicy = extractAdBreakAsWatchedPolicy(_mediaPlayerItem); 
          } 
      
          @Override 
          public AdBreakPolicy selectPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectPolicyForAdBreak", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              if (adPolicyInfo.getAdBreakPlacements().size() > 0) { 
                  AdBreakPlacement adBreakTimelineItem = adPolicyInfo.getAdBreakPlacements().get(0); 
                  if (adPolicyInfo.getMode() == AdPolicyMode.SEEK && adBreakTimelineItem.getAdBreak().isWatched()) { 
                      return AdBreakPolicy.SKIP; 
                  } 
              } 
      
              AdSignalingMode adSignalingMode = AdSignalingMode.DEFAULT; 
              if (_mediaPlayerItem != null) { 
                  MetadataNode metadata = (MetadataNode) _mediaPlayerItem.getResource().getMetadata(); 
                  if (metadata != null) { 
                      AdvertisingMetadata advertisingMetadata = (AdvertisingMetadata) metadata.getNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue()); 
                      if (advertisingMetadata != null) { 
                          adSignalingMode = advertisingMetadata.getSignalingMode(); 
                      } 
                  } 
              } 
      
              // can't remove main content due to a ave bug, need to check if stream is live or ad signaling mode is manifest cue 
              if (_mediaPlayerItem.isLive() || adSignalingMode == AdSignalingMode.MANIFEST_CUES) { 
                  return AdBreakPolicy.PLAY; 
              } 
      
              return AdBreakPolicy.REMOVE_AFTER_PLAY; 
          } 
      
          @Override 
          public List<AdBreakPlacement> selectAdBreaksToPlay(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectAdBreaksToPlay", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              List<AdBreakPlacement> adBreakPlacements = adPolicyInfo.getAdBreakPlacements(); 
              if (adBreakPlacements != null) { 
                  int size = adBreakPlacements.size(); 
                  List<AdBreakPlacement> adBreaks = new ArrayList<AdBreakPlacement>(); 
                  if (size > 0 && adPolicyInfo.getCurrentTime() <= adPolicyInfo.getSeekToTime()) { 
                      AdBreakPlacement adBreak = adBreakPlacements.get(size - 1); 
                      if (!adBreak.getAdBreak().isWatched()) { 
                          adBreaks.add(adBreak); 
                          return adBreaks; 
                      } 
                  } 
              } 
      
              return null; 
          } 
      
          @Override 
          public AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectPolicyForSeekIntoAd", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              // If you really want to allow seek during ads (you likely do not). 
              return AdPolicy.PLAY; 
          } 
      
          @Override 
          public AdBreakAsWatched selectWatchedPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectWatchedPolicyForAdBreak", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              return _adBreakAsWatchedPolicy; 
          } 
      
          /** 
           * Extract the ad break watched policy for the specified media player item. 
           * 
           * @param item Associated media player item. 
           * @return a valid ad break watched policy. 
           */ 
          private AdBreakAsWatched extractAdBreakAsWatchedPolicy(MediaPlayerItem item) { 
              AdBreakAsWatched adBreakWatchedPolicy = AdBreakAsWatched.AD_BREAK_AS_WATCHED_ON_BEGIN; 
      
              if (item != null) { 
                  MetadataNode metadata = (MetadataNode) item.getResource().getMetadata(); 
                  if (metadata != null) { 
                      AdvertisingMetadata advertisingMetadata = (AdvertisingMetadata) metadata.getNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue()); 
                      if (advertisingMetadata != null) { 
                          adBreakWatchedPolicy = advertisingMetadata.getAdBreakAsWatched(); 
                      } 
                  } 
              } 
      
              return adBreakWatchedPolicy; 
          } 
      } 
      ```

   1. 샘플 광고 공장

      ```
      private AdvertisingFactory createPartialAdBreakFactory() { 
      return new AdvertisingFactory() { 
      @Override 
                   public AdPolicySelector  
      createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
                      return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
                   } 
      
      // Rest of the interface methods can be overridden as per your  
      // customization needs 
      // As shown next 
      @Override 
      public AdPolicySelector  
      createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
         return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
        } 
      // . . . 
      
       } 
      } 
      ```

   1. 미디어 플레이어에 AdvertisingFactory 등록

      ```
      AdvertisingFactory advertisingFactory = createPartialAdBreakFactory();  
      
      if (advertisingFactory != null) { 
                  mediaPlayer.registerAdClientFactory(advertisingFactory); 
      } 
      ```

   1. createAdPolicySelector 메서드 재정의

      ```
      @Override 
      public AdPolicySelector  
      createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
         return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
      } 
      ```


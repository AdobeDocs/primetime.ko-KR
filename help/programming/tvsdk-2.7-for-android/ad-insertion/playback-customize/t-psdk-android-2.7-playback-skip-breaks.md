---
description: 기본적으로 TVSDK는 사용자가 광고 브레이크를 검색할 때 광고 브레이크를 강제로 재생합니다. 이전 브레이크 완료에서 경과된 시간이 특정 분 이내인 경우 광고 브레이크를 건너뛰도록 동작을 사용자 지정할 수 있습니다.
title: 일정 기간 동안 광고 브레이크 건너뛰기
exl-id: 13e34c05-2c43-4459-88ec-5c6cfa8c363d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 일정 기간 동안 광고 브레이크 건너뛰기 {#skip-ad-breaks-for-a-period-of-time}

기본적으로 TVSDK는 사용자가 광고 브레이크를 검색할 때 광고 브레이크를 강제로 재생합니다. 이전 브레이크 완료에서 경과된 시간이 특정 분 이내인 경우 광고 브레이크를 건너뛰도록 동작을 사용자 지정할 수 있습니다.

>[!IMPORTANT]
>
>광고를 용서하기 위해 내부 검색을 완료해야 하는 경우 재생 중에 약간 일시 중지가 있을 수 있습니다.

기본 TVSDK 광고 브레이크 동작을 재정의하려면 기본 광고 정책 선택기를 확장할 수 있습니다. 네 가지 광고 브레이크 정책을 사용할 수 있습니다.

* 재생
* 건너뛰기

   >[!NOTE]
   >
   >광고가 라이브 포인트에 있는 경우 SKIP 광고 브레이크 정책이 라이브 스트림에 대해 예상대로 작동하지 않을 수 있습니다. 예를 들어 프리롤의 경우 SKIP을 사용하면 광고 브레이크 끝에 대한 찾기가 발생하며, 이는 라이브 포인트보다 클 수 있습니다. 이 경우, TVSDK는 광고의 가운데로 이동할 수 있습니다.

* REMOVE_AFTER
* 제거

   >[!NOTE]
   >
   >다음 `REMOVE` 광고 브레이크 정책이 사용 중단될 예정입니다. Adobe은 `SKIP` 대신 광고 브레이크 정책 `REMOVE`.

사용자 지정된 광고 정책 선택기의 다음 예제는 사용자가 광고 브레이크를 시청한 후 5분(벽면 시계 시간) 안에 광고를 건너뜁니다.

1. 사용자가 광고 브레이크 보기를 마치면 현재 시스템 시간을 저장합니다.

   ```java
   @Override 
   public void onAdBreakComplete(AdBreak adBreak) { 
       ... 
       if (isShouldPlayUpcomingAdBreakRuleEnabled()) { 
           CustomAdPolicySelector.setLastAdBreakPlayedTime(System.currentTimeMillis()); 
           ... 
       } 
   }
   ```

1. 확장 `AdPolicySelector`.

   ```java
   package com.adobe.mediacore.sample.advertising; 
   
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerItemConfig; 
   import com.adobe.mediacore.timeline.advertising.policy.*; 
   import com.adobe.mediacore.timeline.advertising.AdBreakTimelineItem; 
   import com.adobe.mediacore.metadata.AdvertisingMetadata; 
   
   import java.util.ArrayList; 
   import java.util.List; 
   
   public class CustomAdPolicySelector implements AdPolicySelector { 
   
       private static final long MIN_BREAK_INTERVAL = 300000; // 5 minutes for next ad break to be played 
       private MediaPlayerItem _mediaPlayerItem; 
       private static long _lastAdBreakPlayedTime; 
       private AdBreakWatchedPolicy watchedPolicy = AdBreakWatchedPolicy.WATCHED_ON_BEGIN; 
   
       public CustomAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           _mediaPlayerItem = mediaPlayerItem; 
           _lastAdBreakPlayedTime = 0; 
   
           if (mediaPlayerItem != null) { 
               watchedPolicy = extractWatchedPolicy(mediaPlayerItem.getConfig()); 
           } 
       } 
   
       @Override 
       public AdBreakPolicy selectPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
           if (shouldPlayAdBreaks() && adPolicyInfo.getAdBreakTimelineItems() != null) { 
   
               AdBreakTimelineItem item = adPolicyInfo.getAdBreakTimelineItems().get(0); 
   
               // This condition will remove the pre-roll ad from live stream after watching 
               if (item.getTime() == 0 && _mediaPlayerItem.isLive()) { 
                   return AdBreakPolicy.REMOVE_AFTER_PLAY; 
               } 
               if (item.getTime() == 0) { 
                   return AdBreakPolicy.PLAY; 
               } 
   
               // This condition will remove every ad break that has been watched once.  
               // Comment this section if you want to play watched ad breaks again. 
               if (item.isWatched()) { 
                   return AdBreakPolicy.SKIP; 
               } 
   
               return AdBreakPolicy.REMOVE_AFTER_PLAY; 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       @Override 
       public List<AdBreakTimelineItem> selectAdBreaksToPlay(AdPolicyInfo adPolicyInfo) { 
   
           if (shouldPlayAdBreaks()) { 
   
               List<AdBreakTimelineItem> timelineItems = adPolicyInfo.getAdBreakTimelineItems(); 
               AdBreakTimelineItem item; 
               List<AdBreakTimelineItem> selectedItems = new ArrayList<AdBreakTimelineItem>(); 
   
               if (timelineItems != null && timelineItems.size() > 0) { 
   
                   // Seek Forward Condition 
                   if (adPolicyInfo.getCurrentTime() <= adPolicyInfo.getSeekToTime()) { 
                       item = timelineItems.get(0); 
   
                       // Resume logic - This will be helpful in resuming the content  
                       // from last saved playback session, and just play the pre-roll ad 
                       if(adPolicyInfo.getCurrentTime() == 0) { 
                           if(item.getTime() == 0 && !item.isWatched()) { 
                               // comment this line if you just need to seek to the user's  
                               // last known position without playing pre-roll ad. ZD#820 
                               selectedItems.add(item); 
                               return selectedItems; 
                           } 
                           else{ 
                               return null; 
                           } 
                       } else { 
                           item = timelineItems.get(timelineItems.size()-1); 
                           if (!item.isWatched()) { 
                               selectedItems.add(item); 
                               return selectedItems; 
                           } 
                       } 
   
                       // Seek backward condition 
                   } else if (adPolicyInfo.getCurrentTime() > adPolicyInfo.getSeekToTime()) { 
                       item = timelineItems.get(0); 
   
                       if(!item.isWatched()) { 
                           selectedItems.add(item); 
                           return selectedItems; 
                       } else { 
                           return null; 
                       } 
                   } 
               } 
           } 
           return null; 
       } 
   
       @Override 
       public AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo) { 
           // Simple Ad Policy selector 
           // if the first ad in the break was watched,  
           // skip to the next add after the seek position 
           // otherwise, play the ads in the break from the beginning 
   
           List<AdBreakTimelineItem> timelineItems = adPolicyInfo.getAdBreakTimelineItems(); 
           if (timelineItems != null && timelineItems.size() > 0) { 
               if (timelineItems.get(0).isWatched()) { 
                   return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
               } 
           } 
   
           // Resume play from the next ad in the break 
           return AdPolicy.PLAY_FROM_AD_BREAK_BEGIN; 
   
       } 
   
       @Override 
       public AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
           return watchedPolicy; 
       } 
   
       public static void setLastAdBreakPlayedTime(long lastAdBreakPlayedTime) { 
           _lastAdBreakPlayedTime = lastAdBreakPlayedTime; 
       } 
   
       private boolean shouldPlayAdBreaks() { 
           long currentTime = System.currentTimeMillis(); 
   
           if (_lastAdBreakPlayedTime <= 0) { 
               return true; 
           } 
   
           if (_lastAdBreakPlayedTime > 0 &&  
             (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) { 
               return true; 
           } 
   
           // return false for not playing Ad if this  
           // Ad occurs with 5 minutes of last Ad playback 
           return false; 
       } 
   
       private AdBreakWatchedPolicy extractWatchedPolicy(MediaPlayerItemConfig config) { 
           if (config != null) { 
               AdvertisingMetadata metadata = config.getAdvertisingMetadata(); 
               if (metadata != null) { 
                   return metadata.getAdBreakWatchedPolicy(); 
               } 
           } 
           return AdBreakWatchedPolicy.WATCHED_ON_BEGIN; 
       } 
   } 
   ```

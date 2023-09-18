---
description: TVSDK는 일시 중단 기간 처리를 위한 API 및 샘플 코드를 제공합니다.
title: 일시 중단 처리 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 일시 중단 처리 구현{#implement-blackout-handling}

TVSDK는 일시 중단 기간 처리를 위한 API 및 샘플 코드를 제공합니다.

일시 중단 중에 대체 컨텐츠를 제공하는 등 일시 중단 처리를 구현하려면 다음 작업을 수행하십시오.

1. 라이브 스트림 매니페스트에서 일시 중단 태그를 검색하도록 앱을 설정합니다.

   ```java
   public void createMediaPlayer { 
       ... 
       String[] blackoutTags = {BLACKOUTTAG}; 
       PSDKConfig.setSubscribedTags(blackoutTags); 
       // For example: PTSDKConfig.setSubscribedTags({"#EXT-OATCLS-SCTE35"}); 
   }
   ```

1. 전경 및 배경 스트림에서 시간이 지정된 메타데이터 이벤트에 대한 이벤트 리스너를 만듭니다.

   ```java
   private MediaPlayer createMediaPlayer() { 
       mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, _playbackEventListener); 
       mediaPlayer.addEventListener(MediaPlayer.Event.BLACKOUTS, _blackoutsEventListener); 
   }
   ```

1. 전경 및 백그라운드 스트림 모두에 대해 시간 설정된 메타데이터 이벤트 핸들러를 구현합니다.

   전경:

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
             new MediaPlayer.PlaybackEventListener() { 
       ... 
   
       @override 
       public void onTimedMetadata(TimedMetadata timedMetadata) { 
           if (timedMetadata.getName().equal(BLACKOUTTAG) &&  
               !_timedMetadataList.contains(timedMetadata)) { 
                 _timedMetadataList.add(timedMetadata); 
           } 
       } 
       ... 
   } 
   
   private final MediaPlayer.BlackoutsEventListener _blackoutsEventListener =  
     new MediaPlayer.BlackoutsEventListener() { 
       @Override 
       public void onTimedMetadataInBackgroundItem(TimedMetadata timedMetadata) { 
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.TAG) && _mediaPlayer.getPlaybackRange() != null  
               && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               if (!_timedMetadataList.contains(timedMetadata) && isBlackoutMetadata(timedMetadata)) { 
                   _timedMetadataList.add(timedMetadata); 
               } 
           } 
       } 
   
       @Override 
       public void onBackgroundManifestFailed() { 
           ... 
       } 
   }; 
   ```

1. 핸들 `TimedMetadata` 다음의 경우 오브젝트 `MediaPlayer` 시간이 실행됩니다.

   ```java
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null  
                       && _timedMetadataList.size() > 0) { 
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) { 
                           long localTime = _mediaPlayer.getLocalTime(); 
                           handleTimedMetadataList(localTime);      
                       } 
                   } 
               }                        
           }); 
       } 
   };
   ```

1. 일시 중단 기간 시작 및 종료 시 컨텐츠를 전환하는 방법을 생성합니다.

   ```java
   private void handleTimedMetadataList(long currentTime) { 
       for (int i = 0; i < _timedMetadataList.size(); i++) { 
           TimedMetadata timedMetadata = _timedMetadataList.get(i); 
           long diff = localTime - timedMetadata.getTime(); 
           if (!_timedMetadataDispatchedList.contains(timedMetadata) 
               && diff >= 0 
               && diff <= PLAYBACK_CLOCK_INTERVAL 
               && _mediaPlayer.shouldTriggerSubscribedTagEvent()) { 
                   // switch to blackout content 
               if (!_inBlackout && isBlackoutStartTimedMetadata(timedMetadata)) { 
                   MediaResource blackoutMediaResource = createBlackoutMediaResource(timedMetadata); 
   
                   //1. register current item as background item 
                   _mediaPlayer.registerCurrentItemAsBackgroundItem(); 
   
                   //2. replace current item with blackout item 
                   _mediaPlayer.replaceCurrentItem(blackoutMediaResource); 
   
                   //3. update qos metrics 
                   _mediaQosProvider.updateMetrics(_mediaPlayer); 
   
                   //4. maintain state 
                   _inBlackout = true; 
                   resetTimedMetada(); 
   
                   break; 
               } 
               // switch back to main content 
               else if (_inBlackout && isBlackoutEndTimedMetadata(timedMetadata)) { 
                   //1. register current item as background item 
                   _mediaPlayer.unregisterCurrentBackgroundItem(); 
   
                   //2. replace current item with blackout item 
                   _mediaPlayer.replaceCurrentItem(_oldMediaResource); 
   
                   //3. update qos metrics 
                   _mediaQosProvider.updateMetrics(_mediaPlayer); 
   
                   //4. maintain state 
                   _inBlackout = false; 
                   resetTimedMetada(); 
   
                   break; 
               } 
           } 
       } 
   }
   ```

1. 일시 중단 범위가 재생 스트림에서 DVR에 있는 경우 찾을 수 없는 범위를 업데이트합니다.

   ```java
   // prepare and update blackout nonSeekable ranges 
   
   List<TimeRange> blackoutRanges = prepareBlackoutRanges(_timedMetadataList); 
   if (blackoutRanges != null && blackoutRanges.size() > 0) { 
       int size = blackoutRanges.size(); 
       TimeRange[] blackoutRangesArray = blackoutRanges.toArray(new TimeRange[size]); 
       BlackoutMetadata blackoutMetadata = new BlackoutMetadata(blackoutRangesArray); 
       updateBlackoutMetadata(blackoutMetadata); 
   } 
   
   // function to update blackout metadata 
   private void updateBlackoutMetadata(BlackoutMetadata blackoutMetadata) { 
       MediaPlayerItem currentItem = _mediaPlayer.getCurrentItem(); 
       if (currentItem != null) { 
           Metadata metadata = currentItem.getResource().getMetadata(); 
           if (metadata != null) { 
               MetadataNode metadataNode = ((MetadataNode) metadata); 
               metadataNode.setNode(DefaultMetadataKeys.BLACKOUT_METADATA_KEY.getValue(),  
                                    blackoutMetadata); 
   
               for (int i = 0; i < blackoutMetadata.getNonSeekableRanges().length; i++) { 
                   TimeRange timeRange = blackoutMetadata.getNonSeekableRanges()[i]; 
               } 
           } 
       } 
   }
   ```

   >[!NOTE]
   >
   >현재 여러 비트 전송률 라이브 스트림의 경우, 경우에 따라 조정 가능한 비트 전송률(ABR) 프로필이 동기화되지 않을 수 있습니다. 이로 인해 중복 발생 `timedMetadata` 동일한 구독한 태그에 대한 개체입니다. 검색할 수 없는 잘못된 계산을 방지하려면 다음 예제와 같이 계산 후 검색할 수 없는 범위가 겹치는지 확인하는 것이 좋습니다.

   ```java
   List<TimeRange> rangesToRemove = new ArrayList<TimeRange>(); 
   
   for (int i = 0; i < nonSeekableRanges.size() - 1; i++) { 
       TimeRange range1 = nonSeekableRanges.get(i); 
       TimeRange range2 = nonSeekableRanges.get(i + 1); 
       if (range1.contains(range2.getBegin()) && !rangesToRemove.contains(range2)) { 
          rangesToRemove.add(range2); 
       } else if (range2.contains(range1.getBegin()) && !rangesToRemove.contains(range1)) { 
          rangesToRemove.add(range1); 
      } 
   } 
   
   if (nonSeekableRanges.size() > 0 && rangesToRemove.size() > 0) { 
       nonSeekableRanges.removeAll(rangesToRemove); 
       for (int i = 0; i < rangesToRemove.size(); i++) { 
           TimeRange range = rangesToRemove.get(i); 
       } 
   } 
   
   if (nonSeekableRanges.size() > 0 && rangesToRemove.size() > 0) { 
       nonSeekableRanges.removeAll(rangesToRemove); 
   }
   ```

---
description: 현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.
seo-description: 현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.
seo-title: 시간 지정 메타데이터 사용
title: 시간 지정 메타데이터 사용
uuid: 9bbdaefa-4ac5-4e08-92b4-15ebe5c46864
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# 시간 메타데이터 사용{#use-timed-metadata}

현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.

재생하는 동안 이러한 저장된 `PTTimedMetadata` 개체를 사용하려면 [Store의 저장된 사전(메타데이터 개체가 전달될 때)을 사용합니다](../../../tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-timed-metadata-store.md).

1. 이 알림에서 현재 재생 시간을 추출 및 업데이트하고 현재 재생 시간과 일치하는 시작 시간이 있는 모든 `PTTimedMetadata` 개체를 찾습니다.

   이러한 개체를 사용하여 다양한 작업을 완료할 수 있습니다.

   예:

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       CMTimeRange seekableRange = self.player.seekableRange; 
       if (CMTIMERANGE_IS_VALID(seekableRange)) 
       { 
           int currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
           NSArray *allKeys = timedMetadataCollection ? [timedMetadataCollection allKeys] : [NSArray array]; 
           NSMutableArray *timedMetadatasToDelete = [[[NSMutableArray alloc] init] autorelease]; 
           int count = [allKeys count]; 
   
           for (int i=count - 1; i > -1; i--) 
           { 
              NSNumber *currTimedMetadataTime = allKeys[i]; 
              if ([currTimedMetadataTime integerValue] == currentTime) 
              { 
               /* 
                   Use the timed metadata here and remove it from the collection. 
               */ 
                NSLog (@"IN PLAYBACK TIME %i TO EXECUTE TIMEDMETADATA %@ scheduled at time %f",currentTime,currTimedMetadata.name,CMTimeGetSeconds(currTimedMetadata.time)); 
   
               PTTimedMetadata *currTimedMetadata = [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
               [timedMetadatasToDelete addObject:currTimedMetadataTime]; 
              } 
           } 
   
           for (int i=0; i<[timedMetadatasToDelete count]; i++) 
           { 
               NSNumber *timedMetadataToDelete = timedMetadatasToDelete[i]; 
               [timedMetadataCollection removeObjectForKey:timedMetadataToDelete]; 
           } 
       } 
   }
   ```

1. 메모리가 지속적으로 증가하지 않도록 목록에서 오래된 `PTTimedMetadata` 인스턴스를 주기적으로 플러시합니다.

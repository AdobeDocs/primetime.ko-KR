---
description: 현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.
title: 시간 메타데이터 사용
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# 시간 메타데이터 사용{#use-timed-metadata}

현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.

저장된 값을 사용하려면 `PTTimedMetadata` 재생 중 개체, 저장된 사전 사용 [시간 초과된 메타데이터 개체가 디스패치될 때 저장](../../../tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-timed-metadata-store.md).

1. 이 알림에서 현재 재생 시간을 추출 및 업데이트하고 다음을 모두 찾습니다. `PTTimedMetadata` 시작 시간이 현재 재생 시간과 일치하는 오브젝트.

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

1. 부실 주기적으로 플러시 `PTTimedMetadata` 메모리가 계속 증가하지 않도록 하기 위한 목록의 인스턴스입니다.

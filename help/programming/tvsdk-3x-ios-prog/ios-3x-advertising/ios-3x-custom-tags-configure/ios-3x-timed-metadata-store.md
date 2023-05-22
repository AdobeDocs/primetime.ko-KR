---
description: 응용 프로그램은 적절한 시간에 적절한 PTTimedMetadata 개체를 사용해야 합니다.
title: 시간이 지정된 메타데이터 개체가 발송될 때 이를 저장합니다.
exl-id: 8b859e8d-eb4c-48f9-a95e-1bcc35a2a520
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 시간이 지정된 메타데이터 개체가 발송될 때 이를 저장합니다. {#store-timed-metadata-objects-as-they-are-dispatched}

응용 프로그램은 적절한 시간에 적절한 PTTimedMetadata 개체를 사용해야 합니다.

재생 전에 발생하는 컨텐츠 구문 분석 중에 TVSDK는 구독한 태그를 식별하고 애플리케이션에 이러한 태그에 대해 알립니다. 각 시간과 관련된 시간 `PTTimedMetadata` 는 재생 타임라인의 절대 시간입니다.

애플리케이션은 다음 작업을 완료해야 합니다.

1. 현재 재생 시간을 추적합니다.
1. 현재 재생 시간을 발송된 시간과 일치 `PTTimedMetadata` 개체.

1. 사용 `PTTimedMetadata` 여기서 시작 시간은 현재 재생 시간과 같습니다.

   >[!NOTE]
   >
   >아래 코드는 하나만 있다고 가정합니다. `PTTimedMetadata` 인스턴스를 한 번에 만듭니다. 인스턴스가 여러 개 있는 경우 애플리케이션은 해당 인스턴스를 사전에 적절하게 저장해야 합니다. 한 가지 방법은 주어진 시간에 배열을 만들고 해당 배열의 모든 인스턴스를 저장하는 것입니다.

   다음 예제는 저장 방법을 보여 줍니다 `PTTimedMetadata` 의 오브젝트 `NSMutableDictionary (timedMetadataCollection)` 각각의 시작 시간까지 입력 `timedMetadata`.

   ```
   NSMutableDictionary *timedMetadataCollection; 
   
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       if (!timedMetadataCollection) 
       { 
           timedMetadataCollection = [[NSMutableDictionary alloc] init]; 
       } 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey] retain]; 
       if ([timedMetadata.name  isEqualToString: @"#EXT-OATCLS-SCTE35"]) 
       { 
            NSLog(@"Adding timedMetadata %@ to timedMetadataCollection with time                      
                    %f",timedMetadata.name,CMTimeGetSeconds(timedMetadata.time)); 
   
           NSNumber *timedMetadataStartTime = [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
       [timedMetadata release]; 
   }
   ```

## Nielsen ID3 태그 구문 분석 {#example_3B51E9D4AF2449FAA8E804206F873ECF}

구문 분석을 위해 ID3 태그를 추출하려면 `onMediaPlayerSubscribedTagIdentified` 방법:

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

ID3 태그를 구문 분석한 후 다음을 사용하여 Nielsen 관련 메타데이터를 추출합니다.

```
    (NSString *)parseNielsenUrlFromID3Tag:(NSString *)str 
    { 
    /* ID3 tag <AVMetadataItem: 0x15e58e60, identifier=id3/PRIV, keySpace=org.id3, key class = __NSCFString, key=PRIV, commonKey=(null), extendedLanguageTag=(null), dataType=(null), time= {110265598/4410000 = 25.004} 
 
    , duration= 
    {INVALID} 
 
    , startDate=(null), extras= 
    { info = "www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/pI-X5FFk07770SXf2ZbI6g==/CE0C6​1TsDo0jIrNn9N2yTPe6nVG3dHZHfgS52fJeQjf9fJCga9tj4OW4NXPZ9fI1mx0gfYUPBXnjqolHemZPtn_FCoNg​8Dqw8-Auruf15fU04pJfXTTN0IgZ4iWBmeRiPpS9X100zdCIGeIlgZnkYj6UvVjmPIdY5jyRQTA=/00000/21778/00"; } 
 
    , value length=1> 
    */ 
 
NSString *nielsenStr = nil; 
for (NSString *keyValuePairString in [str componentsSeparatedByString:@", "]) 
{ 
if([keyValuePairString rangeOfString:@"nielsen.com"].location != NSNotFound) 
{ // Nielsen NSRange start = [keyValuePairString rangeOfString:@"\""]; NSRange end = [keyValuePairString rangeOfString:@"\";"]; nielsenStr = [keyValuePairString substringWithRange:NSMakeRange(start.location + 1, end.location-start.location)]; } 
 
} 
return nielsenStr; 
}
```

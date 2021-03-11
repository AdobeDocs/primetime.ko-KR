---
description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
title: 사용자 지정 컨텐츠 해결 프로그램 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# 사용자 지정 내용 확인자 {#implement-a-custom-content-resolver} 구현

기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.

TVSDK에서 새로운 기회를 감지하면 등록된 컨텐츠 해결에서 해당 기회를 해결할 수 있는 기회를 찾습니다. true를 반환한 첫 번째 값이 기회를 해결하기 위해 선택됩니다. 컨텐츠 해결 프로그램을 사용할 수 없는 경우 해당 기회를 건너뜁니다. 컨텐츠 확인 프로세스는 일반적으로 비동기적이므로, 컨텐츠 확인자는 프로세스가 완료되면 이를 알릴 책임이 있습니다.

1. 사용자 지정 `AdvertisingFactory` 인스턴스를 만들고 `createContentResolver`을(를) 재정의합니다.

   예:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public ContentResolver createContentResolver(MediaPlayerItem item) { 
           Metadata metadata = _mediaPlayer.getCurrentItem().getResource().getMetadata(); 
           if (metadata != null) { 
               if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
                   return new AuditudeResolver(getActivity().getApplicationContext()); 
               } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
                   return new MetadataResolver(); 
               } else if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
                   return new CustomAdMarkersContentResolver(); 
               } else if (metadata.containsKey(CustomAdResolver.CUSTOM_METADATA_KEY)) { 
                   return new CustomAdResolver(); 
               } 
           } 
           return null; 
       } 
       ... 
   }
   ```

1. 광고 클라이언트 팩토리를 `MediaPlayer`에 등록합니다.

   예:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 다음과 같이 `AdvertisingMetadata` 개체를 TVSDK에 전달합니다.
   1. `AdvertisingMetadata` 개체 및 `MetadataNode` 개체를 만듭니다.
   1. `AdvertisingMetadata` 개체를 `MetadataNode`에 저장합니다.

   ```java
   MetadataNode result = new MetadataNode(); 
   result.setNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue(),  
                  advertisingMetadata);
   ```

1. `ContentResolver` 클래스를 확장하는 사용자 지정 광고 확인자 클래스를 만듭니다.
   1. 사용자 지정 광고 확인자에서 이 보호된 함수를 재정의합니다.

      ```java
      void doResolveAds(Metadata metadata,  
                        PlacementOpportunity placementOpportunity)
      ```

      메타데이터에 `AdvertisingMetada`이(가) 포함되어 있습니다. 다음 `TimelineOperation` 벡터 생성에 사용합니다.

   1. 각 배치 기회에 대해 `Vector<TimelineOperation>`을(를) 만듭니다.

      벡터는 비어 있을 수 있지만 null은 아닙니다.

      이 샘플 `TimelineOperation`은 `AdBreakPlacement`에 대한 구조를 제공합니다.

      ```java
      AdBreakPlacement(AdBreak.createAdBreak( 
                                ads,       // Vector<Ad> 
                                time,      // Ad Break start time. Note: local time on the timeline 
                                duration,  // Ad Break duration 
                                tag()      // An arbitrary string value that can be attached to  
                                           // the AdBreak object. 
                               ), placementInformation  // Retrieved from PlacementOpportunity 
      )
      ```

   1. 광고가 해결되면 다음 함수 중 하나를 호출합니다.

      * 광고 해결에 성공한 경우:`notifyResolveComplete(Vector<TimelineOperation> proposals)`
      * 광고 해결에 실패하는 경우:`notifyResolveError(Error error)`

      예를 들어, 실패할 경우:

      ```java
      Metadata metadata = new MetadataNode(); 
      metadata.setValue("NATIVE_ERROR_CODE", exception.getCause().toString()); 
      error.setMetadata(metadata);
      ```


<!--<a id="example_4F0D7692A92E480A835D6FDBEDBE75E7"></a>-->

이 샘플 사용자 지정 광고 확인자는 광고 서버에 HTTP 요청을 만들고 JSON 응답을 수신합니다.

```java
public class CustomAdResolver extends ContentResolver { 
    ... 
    @Override 
    protected void doResolveAds(Metadata metadata, PlacementOpportunity placementOpportunity) { 
        ... 
        if (resolveSuccess == true) { 
            notifyResolveComplete(Vector<TimelineOperation> proposals); 
        } 
        else { 
            notifyResolveError(Error error); 
        } 
    } 
    ... 
}
```

라이브 스트림에 대한 샘플 JSON 광고 서버 응답:

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } 
        ] }, 
        { 
            "start": -1, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```

VOD용 JSON 광고 서버 응답 샘플:

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": {  
                } 
            }, 
            { 
                "id": 1002, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/crescent/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset2", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 50000, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 100000000, 
            "ads": [ { 
                "id": 1004, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/camry/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset4", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```


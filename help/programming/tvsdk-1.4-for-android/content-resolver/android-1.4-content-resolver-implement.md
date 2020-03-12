---
description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
seo-description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
seo-title: 사용자 지정 컨텐츠 해결 프로그램 구현
title: 사용자 지정 컨텐츠 해결 프로그램 구현
uuid: 88627fdc-3b68-4a9f-847e-a490ea8e3034
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 지정 컨텐츠 해결 프로그램 구현 {#implement-a-custom-content-resolver}

기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.

TVSDK가 새로운 기회를 감지하면 등록된 컨텐츠 해결에서 해당 기회를 해결할 수 있는 기회를 찾습니다. True를 반환하는 첫 번째 값이 영업 기회를 해결하기 위해 선택됩니다. 컨텐츠 해결 프로그램이 없으면 해당 기회를 건너뜁니다. 컨텐츠 확인 프로세스는 일반적으로 비동기적이므로 컨텐츠 확인자는 프로세스가 완료되면 이를 알릴 책임이 있습니다.

1. 사용자 정의 `AdvertisingFactory` 인스턴스를 만들고 재정의합니다 `createContentResolver`.

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

1. 광고 클라이언트 팩토리를 에 등록합니다 `MediaPlayer`.

   예:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 다음과 같이 객체를 TVSDK에 `AdvertisingMetadata` 전달합니다.
   1. 개체 `AdvertisingMetadata` 및 `MetadataNode` 개체를 만듭니다.
   1. 객체를 `AdvertisingMetadata` 저장할 `MetadataNode`위치.

   ```java
   MetadataNode result = new MetadataNode(); 
   result.setNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue(),  
                  advertisingMetadata);
   ```

1. 클래스를 확장하는 사용자 지정 광고 해결 프로그램 클래스를 `ContentResolver` 만듭니다.
   1. 사용자 지정 광고 확인자에서 이 보호된 함수를 재정의합니다.

      ```java
      void doResolveAds(Metadata metadata,  
                        PlacementOpportunity placementOpportunity)
      ```

      메타데이터에는 사용자가 포함됩니다 `AdvertisingMetada`. 다음 `TimelineOperation` 벡터 생성에 사용합니다.

   1. 각 배치 기회에 대해 를 `Vector<TimelineOperation>`만듭니다.

      벡터는 비어 있을 수 있지만 null은 아닙니다.

      이 샘플에서는 `TimelineOperation` 다음과 같은 구조를 `AdBreakPlacement`제공합니다.

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

   1. 광고가 해결되면 다음 기능 중 하나를 호출합니다.

      * 광고 해결이 성공한 경우: `notifyResolveComplete(Vector<TimelineOperation> proposals)`
      * 광고 결제가 실패하는 경우: `notifyResolveError(Error error)`
      예를 들어, 실패할 경우:

      ```java
      Metadata metadata = new MetadataNode(); 
      metadata.setValue("NATIVE_ERROR_CODE", exception.getCause().toString()); 
      error.setMetadata(metadata);
      ```


<!--<a id="example_4F0D7692A92E480A835D6FDBEDBE75E7"></a>-->

이 샘플 사용자 지정 광고 확인자는 광고 서버에 HTTP 요청을 수행하고 JSON 응답을 수신합니다.

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

VOD에 대한 샘플 JSON 광고 서버 응답:

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


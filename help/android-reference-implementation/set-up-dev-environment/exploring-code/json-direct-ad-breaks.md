---
title: 직접 광고 나누기를 위한 JSON 개체
description: 유형 값이 직접 광고 분할인 경우 JSON 개체에 대해 자세히 설명합니다.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 직접 광고 분할에 대한 JSON 개체{#json-object-for-direct-ad-breaks}

다음 코드 블록은 형식 값이 직접 광고 분할인 경우 자세한 JSON 개체를 정의합니다.

`IFeedItemAdapter:getStreamMetadata()`에서 반환되는 `MetadataNode`에는 `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 유형의 키와 아래의 자세한 JSON 개체 값의 문자열 표현 값을 가진 항목이 포함되어 있습니다.

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 
```

| 속성 | 설명 |
|---|---|
| `tag` | `com.adobe.mediacore.timeline.advertising.AdBreak`의 태그 필드에 매핑되는 문자열. |
| `time` | 광고 분류의 시작 시간을 나타내며 `com.adobe.mediacore.timeline.advertising.AdBreak`의 시간 필드에 매핑됩니다. 0 값은 프리롤 광고를 나타냅니다. |
| `replace` | 광고 나누기 대체 기간을 나타내며 `com.adobe.mediacore.timeline.advertising.AdBreak`의 `replaceDuration` 필드에 매핑됩니다. |
| `ad-list` | 주어진 광고 중단 동안 재생되는 광고 목록은 `com.adobe.mediacore.timeline.advertising.AdBreak`의 `List<Ad>` 필드에 매핑됩니다. |

다음 코드 블록은 ads-list 배열에 대한 JSON 개체를 정의합니다.

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 
```

| 속성 | 설명 |
|---|---|
| `url` | 광고 컨텐츠의 URL을 `com.adobe.mediacore.timeline.advertising.Ad`의 URL 필드에 매핑합니다. |
| `duration` | 광고의 지속 시간(`com.adobe.mediacore.timeline.advertising.Ad`에 있는 기간 필드에 매핑됩니다. |
| `tag` | 설명 문자열입니다. |


---
seo-title: 직접 광고 분할을 위한 JSON 개체
title: 직접 광고 분할을 위한 JSON 개체
uuid: ffb901f4-0a8b-40fe-b6ba-5ffebc324cf2
description: 유형 값이 직접 광고 분할인 경우 JSON 개체에 대한 세부 정보
seo-description: 유형 값이 직접 광고 분할인 경우 JSON 개체에 대한 세부 정보
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 직접 광고 분할을 위한 JSON 개체{#json-object-for-direct-ad-breaks}

다음 코드 블록은 유형 값이 직접 광고 분할일 때 JSON 개체에 대한 세부 사항을 정의합니다.

에서 `MetadataNode` 반환되는 `IFeedItemAdapter:getStreamMetadata()` 항목에는 아래의 세부 JSON 개체 값에 대한 문자열 표현 `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 및 유형의 키가 포함된 항목이 포함되어 있습니다.

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
| `tag` | 의 태그 필드에 매핑되는 `com.adobe.mediacore.timeline.advertising.AdBreak`문자열입니다. |
| `time` | 광고 중단의 시작 시간을 나타내며 의 시간 필드에 매핑합니다 `com.adobe.mediacore.timeline.advertising.AdBreak`. 0 값은 프리롤 광고를 나타냅니다. |
| `replace` | 광고 나누기 대체 기간을 나타내며 의 `replaceDuration` 필드에 매핑됩니다 `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | 지정된 광고 중단 동안 재생할 광고 목록이 의 `List<Ad>` 필드에 매핑됩니다 `com.adobe.mediacore.timeline.advertising.AdBreak`. |

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
| `url` | 광고 컨텐트에 대한 URL이 의 url 필드에 매핑됩니다 `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | 광고의 지속 시간으로, 의 지속 시간 필드에 매핑됩니다 `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | 설명 문자열입니다. |


---
title: 직접 광고 브레이크용 JSON 개체
description: 유형 값이 직접 광고 중단인 경우 JSON 개체에 대해 자세히 설명합니다
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 직접 광고 브레이크용 JSON 개체{#json-object-for-direct-ad-breaks}

다음 코드 블록은 유형 값이 직접 광고 중단인 경우 세부 JSON 개체를 정의합니다.

다음 `MetadataNode` 반환한 사람 `IFeedItemAdapter:getStreamMetadata()` 유형의 키가 있는 항목을 포함합니다. `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 및 아래의 세부 정보 JSON 개체 값의 문자열 표현 값입니다.

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
| `tag` | 의 태그 필드에 매핑되는 문자열 `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | 광고 브레이크의 시작 시간을 나타내며 의 시간 필드에 매핑됩니다. `com.adobe.mediacore.timeline.advertising.AdBreak`. 값이 0이면 프리롤 광고를 나타냅니다. |
| `replace` | 광고 브레이크 바꾸기 기간을 나타내며,에 매핑됩니다. `replaceDuration` 의 필드 `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | 지정된 광고 브레이크 중에 재생할 광고 목록은에 매핑됩니다. `List<Ad>` 의 필드 `com.adobe.mediacore.timeline.advertising.AdBreak`. |

다음 코드 블록은 광고 목록 배열에 대한 JSON 개체를 정의합니다.

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
| `url` | 광고 콘텐츠에 대한 URL은 의 URL 필드에 매핑됩니다. `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | 광고 기간은에서 기간 필드에 매핑됩니다. `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | 설명 문자열입니다. |

---
description: VOD 컨텐츠에 광고를 삽입할 수 있습니다.
seo-description: VOD 컨텐츠에 광고를 삽입할 수 있습니다.
seo-title: 시간 범위를 광고로 바꾸기
title: 시간 범위를 광고로 바꾸기
uuid: 50cdcc06-7df5-414b-95d4-c684bc68dce3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 시간 범위를 광고로 바꾸기{#replace-time-ranges-with-an-ad}

VOD 컨텐츠에 광고를 삽입할 수 있습니다.

이 경우 `TimeRanges` 및 `begin` 에서 `end` 는 타임라인에서 `localTime` 제거됩니다. 그것들은 `AdBreak` To `begin` 로 대체됩니다 `begin+replaceDuration`. 교체 기간이 매개 변수로 존재하지 않으면 서버는 반환된 Adbreak를 결정합니다.

>[!NOTE]
>
>사용자 지정 범위에 대해 항상 특정 대체 기간을 제공해야 합니다. 이 사용자 지정 범위를 대체할 광고가 없는 경우 대체 기간을 0으로 지정합니다.

범위를 Primetime 광고 결정 광고로 바꿉니다.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": 
              "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
                 
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replacement-duration": 15000 
                },
                {
                    "begin": 69000,
                    "end": 99000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 251000,
                    "end": 281000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 514000,
                    "end": 544000,
                    "replacement-duration": 30000
                } ]
            },
            "ad": {
                "targeting": [ {
                    "value": "MulAdsAvail12346",
                    "key": "osmfKeyMulAdsAvail12346"
                } ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - Replace TimeRange with Auditude Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```


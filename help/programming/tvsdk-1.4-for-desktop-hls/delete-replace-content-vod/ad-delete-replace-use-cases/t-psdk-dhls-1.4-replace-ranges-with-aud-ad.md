---
description: 'null'
seo-description: 'null'
seo-title: 시간 범위를 Adobe Primetime 광고 결정 광고로 바꾸기
title: 시간 범위를 Adobe Primetime 광고 결정 광고로 바꾸기
uuid: 101ac42d-5ba5-4487-af95-483a6594808a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 시간 범위를 Adobe Primetime 광고 결정 광고로 바꾸기{#replace-time-ranges-with-an-adobe-primetime-ad-decisioning-ad}

타임라인에서 `TimeRanges` 및 `begin` 에서 `end` `localTime` 을 제거합니다. AdBreak to로 `begin` 대체합니다 `begin+replaceDuration`.

범위를 Primetime 광고 결정 광고로 바꿉니다.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": "https://. . ./cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replace-duration": 15000
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


---
description: 타임라인에서 localTime의 시작과 끝 사이의 TimeRange를 제거할 수 있습니다.
seo-description: 타임라인에서 localTime의 시작과 끝 사이의 TimeRange를 제거할 수 있습니다.
seo-title: 범위 삭제
title: 범위 삭제
uuid: 2f4afa0d-69e3-4929-8dbd-b553c8a64d96
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# 범위 삭제{#delete-ranges}

타임라인에서 localTime의 시작과 끝 사이의 TimeRange를 제거할 수 있습니다.

>[!NOTE]
>
>컨텐츠에서 특정 범위만 제거하려는 경우 광고 서버가 정의한 대로 광고 맵을 사용해야 하는 경우 `CustomRangeMetadata` 인스턴스를 만들고 정의된 사용자 지정 범위를 가진 DELETE 작업으로 유형을 지정합니다.

Adobe Primetime 광고 결정 광고가 있는 범위를 삭제합니다.

```
{   
    "properties": [],
    "stream": {
        "manifests": [
            {
                "url": "https://xyz.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                "type": "hls"
            }
        ],
     
        "metadata": {
            "time-ranges": {
                "type": "delete",
                "time-range-list": [
                    {
                        "begin": 0,
                        "end": 20000
                    },
                    {
                        "begin": 69000,
                        "end": 99000
                    },
                    {
                        "begin": 251000,
                        "end": 281000
                    },
                    {
                        "begin": 514000,
                        "end": 544000
                    }
                ]
     
            },
            "ad": {
                "targeting": [
                    {
                        "value": "MulAdsAvail12346",
                        "key": "osmfKeyMulAdsAvail12346"
                    }
                ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - DELETE TimeRange with Primetime ad decisioning Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```


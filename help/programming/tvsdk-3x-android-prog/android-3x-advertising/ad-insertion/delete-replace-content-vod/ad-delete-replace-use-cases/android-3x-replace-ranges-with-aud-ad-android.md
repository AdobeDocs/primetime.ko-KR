---
description: VOD 컨텐츠에 광고를 삽입할 수 있습니다.
seo-description: VOD 컨텐츠에 광고를 삽입할 수 있습니다.
seo-title: 시간 범위를 광고로 바꾸기
title: 시간 범위를 광고로 바꾸기
uuid: c1d93389-cba4-4db0-877d-dbdc5183683c
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 시간 범위를 광고로 바꾸기 {#replace-time-ranges-with-an-ad}

VOD 컨텐츠에 광고를 삽입할 수 있습니다.

의 `TimeRanges` 간격은 `begin` 타임라인에서 `end` `localTime` 제거됩니다. 이러한 범위는 `AdBreak` 의 `begin` 범위로 대체됩니다 `begin+replaceDuration`. 매개 변수로 존재하지 `replacement-duration` 않는 경우 서버는 반환된 값을 결정합니다 `Adbreak`.

>[!TIP]
>
>항상 사용자 지정 범위에 `replacement-duration` 대해 a를 제공해야 합니다. 이 사용자 지정 범위를 대체할 광고가 없는 경우 0 `replacement-duration` 을 입력합니다.

1. 범위를 Primetime 광고 결정 광고로 바꾸려면 다음을 수행합니다.

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                   "type": "hls"
               }
           ],
           "metadata": {
               "time-ranges": {
                   "type": "replace",
                   "time-range-list": [
                       {
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
       "title": "VOD - Replace TimeRange with Auditude Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   }
   ```

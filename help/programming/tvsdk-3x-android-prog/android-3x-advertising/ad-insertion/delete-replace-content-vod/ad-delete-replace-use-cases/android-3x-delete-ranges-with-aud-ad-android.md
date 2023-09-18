---
description: 타임라인에서 localTime의 시작과 끝 사이의 TimeRange를 제거할 수 있습니다.
title: 범위 삭제
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 범위 삭제 {#delete-ranges}

다음을 제거할 수 있습니다. `TimeRanges` 사이 `begin` 및 `end` 위치: `localTime` 타임라인에서.

>[!TIP]
>
>콘텐츠에서 특정 범위만 제거하려면 `CustomRangeMetadata` 인스턴스를 참조하고 유형을 다음으로 지정 `DELETE` 정의된 사용자 지정 범위로 작업합니다.

광고 서버에서 정의한 대로 광고 맵을 사용해야 합니다.

1. Adobe Primetime ad decisioning 광고가 있는 범위를 삭제하려면:

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
       "title": "VOD - DELETE TimeRange with xm-replace_text Phrase Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   },
   ```

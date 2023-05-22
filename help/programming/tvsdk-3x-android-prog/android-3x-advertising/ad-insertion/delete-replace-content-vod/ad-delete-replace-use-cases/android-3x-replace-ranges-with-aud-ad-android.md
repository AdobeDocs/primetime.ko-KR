---
description: VOD 콘텐츠에 광고를 삽입할 수 있습니다.
title: 시간 범위를 광고로 바꾸기
exl-id: bee5308a-f867-4824-84a8-751746785971
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 시간 범위를 광고로 바꾸기 {#replace-time-ranges-with-an-ad}

VOD 콘텐츠에 광고를 삽입할 수 있습니다.

다음 `TimeRanges` 다음 사이 `begin` 및 `end` 위치: `localTime` 타임라인에서 제거됩니다. 이 범위는 다음으로 대체됩니다. `AdBreak` / `begin` 끝 `begin+replaceDuration`. 다음과 같은 경우 `replacement-duration` 가 매개 변수로 존재하지 않으면 서버는 반환된 항목에 대해 `Adbreak`.

>[!TIP]
>
>항상 을(를) 제공해야 합니다. `replacement-duration` 사용자 지정 범위용입니다. 이 사용자 지정 범위를 대체할 광고가 없는 경우 `replacement-duration` / 0.

1. 범위를 Primetime ad decisioningAds로 바꾸려면 다음을 수행하십시오.

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

---
description: 'null'
seo-description: 'null'
seo-title: 특별 사용 사례
title: 특별 사용 사례
uuid: 066bc256-4fdf-4083-b23e-0a916b3b532f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 특수 사용 사례{#special-use-cases}

TVSDK는 표준 광고 설정에 비해 사용자 지정 범위 설정을 선호합니다. 예를 들어 MARK 범위가 정의된 경우 광고의 삽입 설정이 무시됩니다. REPLACE 범위가 정의된 경우 TVSDK는 자동으로 `CustomRanges` 신호 모드를 사용합니다.

1. `ReplaceRange` 교체 기간 없음

   교체 기간이 없는 경우 서버에 의해 실제 교체 기간이 결정됩니다. 이 `AdBreak`에 배치된 광고 수도 서버에 의해 결정됩니다.

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   ```

1. 교체 기간이 있는 표시 및 DELETE 범위

   대체 기간이 더 길지 않습니다.

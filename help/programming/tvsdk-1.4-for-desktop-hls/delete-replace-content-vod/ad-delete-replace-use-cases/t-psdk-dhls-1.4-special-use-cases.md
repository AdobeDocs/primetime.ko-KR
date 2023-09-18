---
title: 특별 사용 사례
description: 특별 사용 사례
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 특별 사용 사례{#special-use-cases}

TVSDK는 표준 광고 설정보다 사용자 지정 범위 설정을 선호합니다. 예를 들어 MARK 범위가 정의된 경우 광고의 삽입 설정은 무시됩니다. REPLACE 범위가 정의된 경우 TVSDK는 자동으로 `CustomRanges` 신호 모드.

1. `ReplaceRange` 대체 기간 제외

   교체 기간이 누락된 경우 실제 교체 기간은 서버에 의해 결정됩니다. 여기에 게재된 광고 수 `AdBreak` 또한 서버에 의해 결정됩니다.

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

1. 대체 기간을 사용하여 범위 표시 및 DELETE

   추가 교체 기간은 무시됩니다.

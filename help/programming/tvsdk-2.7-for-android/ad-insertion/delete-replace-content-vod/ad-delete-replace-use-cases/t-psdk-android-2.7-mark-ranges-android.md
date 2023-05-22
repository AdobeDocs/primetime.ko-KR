---
description: VOD 콘텐츠에서 시간 간격을 광고 브레이크로 지정할 수 있습니다.
title: 범위 표시
exl-id: ed13168d-5ee8-4f4b-a72e-a38b6d7f9a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 범위 표시 {#mark-ranges}

VOD 콘텐츠에서 시간 간격을 광고 브레이크로 지정할 수 있습니다.

다음 `TimeRanges` 다음 사이 `begin` 및 `end` 위치: `localTime` 이(가) (으)로 표시됩니다. `AdBreak` 타임라인에서. 다른 광고 설정은 무시됩니다.

>[!TIP]
>
>콘텐츠의 특정 범위만 광고로 표시하고 동적 광고 삽입 기능을 사용하지 않으려면 `CustomRangeMetadata` 인스턴스를 참조하고 형식을 `MARK` 정의된 사용자 지정 범위로 작업합니다.

1. 범위를 표시하려면 다음을 수행합니다.

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
                   "type": "mark",
               "adjust-seek-position" : true,   
                   "time-range-list": [
                     {
                        "begin": 0,
                        "end": 15000
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
   
                 }
            }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   ```

---
description: VOD 컨텐츠의 시간 간격을 광고 중단으로 지정할 수 있습니다.
title: 표시 범위
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# 표시 범위 {#mark-ranges}

VOD 컨텐츠의 시간 간격을 광고 중단으로 지정할 수 있습니다.

`localTime`의 `begin`과 `end` 사이의 `TimeRanges`은 타임라인에서 `AdBreak`로 표시됩니다. 다른 광고 설정은 무시됩니다.

>[!TIP]
>
>동적 광고 삽입 없이 컨텐츠의 특정 범위를 광고로만 표시하려면 `CustomRangeMetadata` 인스턴스를 만들고 정의된 사용자 지정 범위를 사용하여 `MARK` 작업으로 유형을 지정합니다.

1. 범위를 선택합니다.

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


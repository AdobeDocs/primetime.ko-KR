---
description: VOD 콘텐츠에서 시간 간격을 광고 브레이크로 지정할 수 있습니다.
title: 범위 표시
exl-id: cd661327-20b2-4a49-8002-6ecee86c2a2c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 범위 표시{#mark-ranges}

VOD 콘텐츠에서 시간 간격을 광고 브레이크로 지정할 수 있습니다.

이 경우, `TimeRanges` 다음 사이 `begin` 및 `end` 위치: `localTime` 이(가) (으)로 표시됩니다. `AdBreak` 타임라인에서. 다른 광고 설정은 무시됩니다.

>[!NOTE]
>
>콘텐츠의 특정 범위만 광고로 표시하려는 경우(동적 광고 삽입 없음) `CustomRangeMetadata` 을 클릭하고 유형을 정의된 사용자 지정 범위의 MARK 작업으로 지정합니다.

1. 범위를 표시합니다.

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "time-ranges": {
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
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
                    } ]
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

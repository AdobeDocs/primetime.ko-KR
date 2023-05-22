---
title: 범위 표시
description: 범위 표시
copied-description: true
exl-id: 173769cd-6580-4461-9dbc-5bb2fed346d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '24'
ht-degree: 0%

---

# 범위 표시{#mark-ranges}

표시 `TimeRanges` 다음 사이 `begin` 및 `end` 위치: `localTime` as a `AdBreak` 타임라인에서. 다른 광고 설정은 무시됩니다.

1. 시간 범위를 표시합니다.

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

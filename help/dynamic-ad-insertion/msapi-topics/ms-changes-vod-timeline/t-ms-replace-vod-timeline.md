---
description: 매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 보내 VOD 타임라인을 교체합니다.
seo-description: 매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 보내 VOD 타임라인을 교체합니다.
seo-title: VOD 타임라인 교체
title: VOD 타임라인 교체
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# VOD 타임라인 {#replace-a-vod-timeline} 교체

매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 보내 VOD 타임라인을 교체합니다.

1. 일반적인 방법으로 광고 삽입 요청을 준비합니다.
1. `ptcueformat` 쿼리 매개 변수를 DKPIcte35로 설정합니다.
1. `enableC3` 쿼리 매개 변수를 적절하게 true 또는 false로 설정합니다.
1. VOD 타임라인 형식을 사용하여 `pttimeline` 매개 변수를 만듭니다.
   1. 각 컨텐츠 블록(장)을 `duration = 0` 및 `number_of_lots = 1`으로 지정합니다.
   1. 각 광고 블록을 평소대로 지정하지만 `lots = 0`으로 설정하여 중단이 제거됩니다. 광고 중단 지속 시간(M3U8 파일에서)을 사용하려면 `duration = 0`을 설정합니다.

## 예:VOD 타임라인 교체

이 예에서는 VOD 컨텐츠가 `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`의 타임라인과 함께 `Original.m3u8`에 있다고 가정합니다

다음 매니페스트 서버 요청은 `Original.m3u8`의 중단이 30초 프리롤로 바뀌고, 2분 간격으로 2회 분씩 단축됩니다.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

다음 매니페스트 서버 요청은 `Original.m3u8`의 중단점을 제거하고 30초 프리롤과 30초 포스트롤을 추가합니다.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```

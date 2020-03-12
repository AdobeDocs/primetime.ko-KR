---
description: 매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 보내 VOD 타임라인을 교체합니다.
seo-description: 매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 보내 VOD 타임라인을 교체합니다.
seo-title: VOD 타임라인 바꾸기
title: VOD 타임라인 바꾸기
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# VOD 타임라인 바꾸기 {#replace-a-vod-timeline}

매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 보내 VOD 타임라인을 교체합니다.

1. 일반적인 방법으로 광고 삽입 요청을 준비합니다.
1. 쿼리 매개 변수를 DPScte35로 `ptcueformat` 설정합니다.
1. 적절한 경우 `enableC3` 쿼리 매개 변수를 true 또는 false로 설정합니다.
1. VOD 타임라인 포맷을 사용하여 `pttimeline` 매개 변수를 만듭니다.
   1. 및 으로 각 컨텐츠 블록(장)을 `duration = 0` 지정합니다 `number_of_lots = 1`.
   1. 각 광고 블록을 평소대로 지정하지만 중단점을 `lots = 0` 제거하도록 설정합니다. 광고 `duration = 0` 중단의 지속 시간(M3U8 파일에서)을 사용하도록 설정합니다.

## 예:VOD 타임라인 교체

이 예에서는 VOD 컨텐츠가 `Original.m3u8``C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

다음 매니페스트 서버 요청은 30초 프리롤로 중단되는 `Original.m3u8` 것을 대체하며, 그 다음에 2분 간격으로 지속 시간이 두 번 중단됩니다.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

다음 매니페스트 서버 요청은 중단점을 제거하고 30초 프리롤과 30초 포스트롤을 `Original.m3u8` 추가합니다.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```

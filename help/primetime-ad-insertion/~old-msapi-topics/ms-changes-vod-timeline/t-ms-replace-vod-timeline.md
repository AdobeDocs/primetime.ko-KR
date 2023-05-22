---
description: 매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 전송하여 VOD 타임라인을 바꾸십시오.
title: VOD 타임라인 바꾸기
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# VOD 타임라인 바꾸기 {#replace-a-vod-timeline}

매니페스트 서버에 새 광고 삽입 요청을 적절하게 설정된 pttimeline 쿼리 매개 변수로 전송하여 VOD 타임라인을 바꾸십시오.

1. 일반적인 방법으로 광고 삽입 요청을 준비합니다.
1. 설정 `ptcueformat` dpisCTE35에 대한 쿼리 매개 변수입니다.
1. 설정 `enableC3` 매개 변수를 true 또는 false로 적절하게 쿼리합니다.
1. 만들기 `pttimeline` vod 타임라인 형식을 사용하는 매개 변수:
   1. 다음을 사용하여 각 콘텐츠 블록(챕터) 지정 `duration = 0` 및 `number_of_lots = 1`.
   1. 각 광고 블록을 평소대로 지정하되 설정합니다. `lots = 0` 브레이크를 제거합니다. 설정 `duration = 0` 광고 브레이크 기간(M3U8 파일에서)을 사용합니다.

## 예: VOD 타임라인 바꾸기

이 예제는 VOD 콘텐츠가 `Original.m3u8` 다음의 타임라인으로 `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

다음 매니페스트 서버 요청은 의 분리를 대체합니다 `Original.m3u8` 30초 프리롤 후, 2분씩 2번의 지속 시간이 있습니다.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

다음 매니페스트 서버 요청은에서 분리를 제거합니다. `Original.m3u8` 30초 프리롤 및 30초 포스트롤을 추가합니다.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```

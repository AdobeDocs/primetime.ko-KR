---
title: 사용자 지정된 VOD 에셋의 예
description: 사용자 지정된 VOD 에셋의 예
copied-description: true
exl-id: eb6b8438-11b4-4199-8186-d81b3797bfaa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 사용자 지정된 VOD 에셋의 예{#example-of-a-customized-vod-asset}

다음은 사용자 지정된 VOD 에셋의 예입니다.

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

응용 프로그램에서 설정할 수 있는 시나리오는 다음과 같습니다.

* 다음의 경우에 대한 알림 `#EXT-X-ASSET` 태그 또는 구독한 기타 사용자 지정 태그 이름 세트가 파일에 있습니다.
* 다음 경우에 광고 삽입 `#EXT-X-AD` 태그나 다른 모든 사용자 지정 태그 이름은 스트림에서 찾을 수 있습니다.

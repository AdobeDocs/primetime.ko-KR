---
seo-title: 사용자 지정된 VOD 자산의 예
title: 사용자 지정된 VOD 자산의 예
uuid: 1db76b3f-b57a-428a-b79f-d4657ded8391
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# 사용자 지정된 VOD 자산{#example-of-a-customized-vod-asset} 예

사용자 지정된 VOD 자산의 예는 다음과 같습니다.

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

애플리케이션은 다음 시나리오를 설정할 수 있습니다.

* `#EXT-X-ASSET` 태그 또는 구독한 다른 사용자 지정 태그 이름 세트가 파일에 있을 때의 알림.
* 스트림에서 `#EXT-X-AD` 태그 또는 기타 사용자 지정 태그 이름이 발견되면 광고를 삽입합니다.


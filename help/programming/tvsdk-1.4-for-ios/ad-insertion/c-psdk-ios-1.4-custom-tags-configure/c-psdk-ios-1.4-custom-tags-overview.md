---
seo-title: 사용자 지정된 VOD 자산의 예
title: 사용자 지정된 VOD 자산의 예
uuid: e0dfaa72-d62f-4fb3-b7c5-ad94f0dc7ce0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 지정된 VOD 자산의 예{#example-of-a-customized-vod-asset}

다음은 사용자 지정된 VOD 자산의 예입니다.

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

응용 프로그램에서 다음 시나리오를 설정할 수 있습니다.

* 태그 또는 구독한 기타 모든 사용자 지정 태그 이름 세트가 파일에 있을 때의 알림. `#EXT-X-ASSET`
* 스트림에서 `#EXT-X-AD` 태그 또는 다른 사용자 지정 태그 이름이 발견될 때 광고를 삽입합니다.


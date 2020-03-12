---
seo-title: 사용자 지정된 VOD 자산의 예
title: 사용자 지정된 VOD 자산의 예
uuid: 25927d5f-ac16-45f4-bf0d-92f1ab394c05
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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


---
title: 사용자 지정된 VOD 자산의 예
description: 사용자 지정된 VOD 자산의 예
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# 사용자 지정된 VOD 자산 {#example-of-a-customized-vod-asset} 예

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

* `#EXT-X-ASSET` 태그 또는 가입한 다른 사용자 지정 태그 이름 세트가 파일에 있을 때의 알림.
* 스트림에서 `#EXT-X-AD` 태그 또는 다른 사용자 지정 태그 이름이 발견되면 광고를 삽입합니다.


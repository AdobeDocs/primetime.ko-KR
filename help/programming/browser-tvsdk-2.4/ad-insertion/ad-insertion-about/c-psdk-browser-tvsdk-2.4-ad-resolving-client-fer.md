---
description: FER(전체 이벤트 재생) 콘텐츠는 매니페스트 파일의 끝에
title: FER 광고 해결 및 삽입
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# FER 광고 해결 및 삽입{#fer-ad-resolving-and-insertion}

FER(전체 이벤트 재생) 콘텐츠는 매니페스트 파일의 끝에 #EXT-X-ENDLIST 태그를 추가하여 VOD로 변환된 라이브 스트림입니다. 스트림은 광고 큐 마커를 유지합니다.

브라우저 TVSDK는 FER 스트림을 VOD로 처리하므로 기본적으로 광고 시그널링 모드는 입니다. `SERVER_MAP`. 그러나 스트림은 광고 큐 마커를 유지하므로 광고 신호 모드를 로 설정할 수 있습니다 `MANIFEST_CUES`: 광고 삽입에 광고 큐 마커를 사용할 수 있습니다.

FER 스트림에 대한 큐 마커를 사용하여 광고 삽입을 켜려면 다음을 수행하십시오.

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER 광고 해결 및 삽입 동작은 라이브 광고 해결 및 삽입과 유사합니다. 브라우저 TVSDK는 다음을 수행합니다.

1. 콘텐츠의 시작 부분에 프리롤 광고를 삽입합니다.
1. 매니페스트에 정의된 큐 포인트에 의해 지정된 광고를 확인합니다.
1. 기본 컨텐츠의 일부를 동일한 기간의 광고 브레이크로 바꿉니다.
1. 필요한 경우 가상 타임라인을 다시 계산합니다.

**제한 사항:** 브라우저 TVSDK는 HLS FER 스트림 재생만 지원합니다. 또한 MP4 미드롤 광고는 FER 스트림에서 지원되지 않습니다.

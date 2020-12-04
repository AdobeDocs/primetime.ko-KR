---
description: 'FER(Full Event Replay) 컨텐츠는 매니페스트 파일의 끝에 #EXT-X-ENDLIST 태그를 추가하여 VOD로 변환된 라이브 스트림입니다. 스트림에는 광고 큐 마커가 유지됩니다.'
seo-description: 'FER(Full Event Replay) 컨텐츠는 매니페스트 파일의 끝에 #EXT-X-ENDLIST 태그를 추가하여 VOD로 변환된 라이브 스트림입니다. 스트림에는 광고 큐 마커가 유지됩니다.'
seo-title: FER 광고 해결 및 삽입
title: FER 광고 해결 및 삽입
uuid: 85da0e92-17fe-4001-a53c-085dadd09756
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# FER 광고 확인 및 삽입{#fer-ad-resolving-and-insertion}

FER(Full Event Replay) 컨텐츠는 매니페스트 파일의 끝에 #EXT-X-ENDLIST 태그를 추가하여 VOD로 변환된 라이브 스트림입니다. 스트림에는 광고 큐 마커가 유지됩니다.

브라우저 TVSDK는 FER 스트림을 VOD로 취급하므로 기본적으로 광고 신호 모드는 `SERVER_MAP`입니다. 그러나 스트림에 광고 큐 마커가 유지되므로 광고 신호 모드를 `MANIFEST_CUES`으로 설정하여 광고 삽입에 광고 큐 마커를 사용할 수 있습니다.

FER 스트림용 큐 마커를 사용하여 광고 삽입을 켜려면

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER 광고 및 삽입 비헤이비어는 라이브 광고 확인 및 삽입과 유사합니다. 브라우저 TVSDK는 다음을 수행합니다.

1. 콘텐츠 시작 부분에 모든 프리롤 광고를 삽입합니다.
1. 매니페스트에 정의된 큐 포인트로 지정된 광고를 확인합니다.
1. 기본 컨텐츠의 일부를 동일한 기간의 광고 중단으로 대체
1. 필요한 경우 가상 타임라인을 다시 계산합니다.

**제한:** 브라우저 TVSDK는 HLS FER 스트림 재생만 지원합니다. 또한 MP4 중롤 광고는 FER 스트림에서 지원되지 않습니다.

---
description: 컨텐츠가 재생되는 경우 Browser TVSDK는 MediaResource 객체를 만들 때 광고를 표시하고 광고에 대한 정보를 전달할 수 있습니다.
seo-description: 컨텐츠가 재생되는 경우 Browser TVSDK는 MediaResource 객체를 만들 때 광고를 표시하고 광고에 대한 정보를 전달할 수 있습니다.
seo-title: 광고
title: 광고
uuid: 9a5e8c83-18ce-41e8-9cb1-fdc9da903faf
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# 개요 {#ads-overview}

컨텐츠가 재생되는 경우 Browser TVSDK는 MediaResource 객체를 만들 때 광고를 표시하고 광고에 대한 정보를 전달할 수 있습니다.

`AdobePSDK.MediaPlayerStatus.INITIALIZED`을 받은 후 `prepareToPlay` 함수를 호출할 수도 있습니다.

```js
function onStatusChange (event) { 
   switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
        player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
        break; 
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
        player.play(); 
        break; 
   } 
} 
 
var auditudeSettings     = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.domain  = "sample_auditude_domain"; 
auditudeSettings.mediaId = "sample_media_id"; 
auditudeSettings.zoneId  = "sample_zone_id"; 
 
// event handler 
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
 
var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
```

또한 브라우저 TVSDK는 광고가 재생될 때 컨텐츠가 빨리 전달되지 않도록 하기 위해 이벤트 핸들러에서 사용할 수 있는 다음과 같은 광고 관련 이벤트를 제공합니다.

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

UI 프레임워크에서 이 작업을 보려면 다음과 같이 구성에 광고 설정을 지정합니다.

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource: { 
 
            resourceUrl:'Specify Resource Url', 
 
            auditudeSettings: { 
                validMimeTypes: ["application/x-mpeURL"], 
                domain: "Sample_auditude_domain", 
                mediaId:"sample_media_id", 
                zoneID:"sample_zone_id", 
                creativeRepackagingEnabled:true 
            } 
        } 
    } 
}; 
```

필요한 `AuditudeSettings`에 대한 자세한 내용은 [광고 삽입 메타데이터](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md)를 참조하십시오.

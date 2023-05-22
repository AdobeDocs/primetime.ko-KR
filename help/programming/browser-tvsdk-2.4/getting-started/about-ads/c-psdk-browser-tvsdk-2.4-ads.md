---
description: 콘텐츠가 재생될 때 브라우저 TVSDK는 광고를 표시하고 MediaResource 개체를 만들 때 광고에 대한 정보를 전달할 수 있습니다.
title: 광고
exl-id: a44ad0fa-841f-474b-89f4-39666190231f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# 개요 {#ads-overview}

콘텐츠가 재생될 때 브라우저 TVSDK는 광고를 표시하고 MediaResource 개체를 만들 때 광고에 대한 정보를 전달할 수 있습니다.

필요에 따라 `prepareToPlay` 받은 후 함수 `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

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

브라우저 TVSDK는 또한 이벤트 핸들러에 사용하여 광고가 재생될 때 콘텐츠가 빠르게 전달되지 않도록 할 수 있는 다음과 같은 광고 관련 이벤트를 제공합니다.

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

UI 프레임워크에서 작동하는 것을 보려면 다음과 같이 구성에서 광고 설정을 지정합니다.

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

필요한 항목에 대한 자세한 정보 `AuditudeSettings`, 참조 [광고 삽입 메타데이터](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md).

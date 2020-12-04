---
description: 사용자의 현재 라이브 포인트 이후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 전에 발생하는 광고를 해결할지 여부를 결정할 수 있습니다.
seo-description: 사용자의 현재 라이브 포인트 이후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 전에 발생하는 광고를 해결할지 여부를 결정할 수 있습니다.
seo-title: DVR 창에 광고 로드
title: DVR 창에 광고 로드
uuid: 3ae1fbf6-deae-4f39-a17d-43d1fe3cb975
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# DVR 창 {#load-ad-for-a-dvr-window}에 대한 광고 로드

사용자의 현재 라이브 포인트 이후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 전에 발생하는 광고를 해결할지 여부를 결정할 수 있습니다.

사용자가 DVR 스트림 시작 시 컨텐츠를 보기 시작하면 TVSDK는 해당 시간에 해당 스트림에 대한 모든 광고를 확인합니다. 그러나 사용자가 스트림 시작 후 특정 지점에서 컨텐츠를 보기 시작할 때 사용자의 현재 라이브 포인트 이후에 발생하는 광고만 해결할지 또는 현재 라이브 지점 전에 발생한 광고를 해결할지 여부를 결정할 수 있습니다.

>[!TIP]
>
>현재 라이브 포인트 이후 광고를 해결하는 것이 더 빠릅니다. 하지만 사용자가 뒤로 이동하는 경우 이 옵션을 사용하면 플레이어가 이전에 표시된 광고를 재생하지 못합니다.

## DVR 창 {#section_2D93E2E947644D66B6F6ED1DD6742C25}에 대한 컨트롤 및 로드

DVR 창에 대한 광고 로드를 제어하려면

    전체 스트림에 대한 모든 광고를 로드하려면 &#39;PTAdMetadata.enableDVRAds&#39; 속성을 &#39;YES&#39;로 설정합니다.

>[!NOTE]
>
>기본값은 `NO`이며 이 옵션은 현재 라이브 포인트에서 광고만 로드합니다.

예:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
 
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
adMetadata.zoneId = <ZoneId>; 
adMetadata.domain = <Domain>; 
 
// Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
// (PTAuditudeMetadata is a subclass of PTAdMetadata)  
adMetadata.enableDVRAds = YES; 
 
[metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
 
//Create PTMediaPlayerItem with the previously prepared metadata    
playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
```

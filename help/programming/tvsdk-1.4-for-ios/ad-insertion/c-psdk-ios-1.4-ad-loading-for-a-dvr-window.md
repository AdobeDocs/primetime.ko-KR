---
description: 사용자의 현재 라이브 포인트 이후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 이전에 발생하는 광고도 해결할지 여부를 결정할 수 있습니다.
title: DVR 창에 대한 광고 로드
exl-id: f0799002-5cba-41c2-86bb-9ccf6b906357
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# DVR 창에 대한 광고 로드 {#load-ad-for-a-dvr-window}

사용자의 현재 라이브 포인트 이후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 이전에 발생하는 광고도 해결할지 여부를 결정할 수 있습니다.

사용자가 DVR 스트림의 시작 부분에서 콘텐츠를 보기 시작하면 TVSDK는 해당 시간에 스트림에 대한 모든 광고를 확인합니다. 그러나 사용자가 스트림 시작 후 지점에서 컨텐츠를 보기 시작하면 사용자의 현재 라이브 포인트 이후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 전에 발생한 광고도 해결할지 여부를 결정할 수 있습니다.

>[!TIP]
>
>현재 라이브 포인트 이후의 광고를 해결하는 것이 더 빠르지만 사용자가 뒤로 이동하는 경우 이 옵션을 사용하면 플레이어가 이전에 표시된 광고를 재생할 수 없습니다.

## DVR 창에 대한 광고 로드 제어 {#section_2D93E2E947644D66B6F6ED1DD6742C25}

DVR 창에 대한 광고 로드를 제어하려면 다음을 수행합니다.

전체 스트림에 대한 모든 광고를 로드하려면 `PTAdMetadata.enableDVRAds` 다음으로 속성: `YES`.

>[!NOTE]
>
>기본값은 입니다. `NO`, 그리고 이 옵션은 현재 라이브 포인트에서만 광고를 로드합니다.

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

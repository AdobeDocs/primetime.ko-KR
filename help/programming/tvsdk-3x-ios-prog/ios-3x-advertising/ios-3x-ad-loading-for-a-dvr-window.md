---
description: 사용자의 현재 라이브 포인트 후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 전에 발생하는 광고를 해결할지 여부를 결정할 수 있습니다.
title: DVR 창에 대한 광고 로드
exl-id: 3e8542a8-0912-4023-904d-0fdb28411a9d
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# DVR 창에 대한 광고 로드 {#load-ad-for-a-dvr-window}

사용자의 현재 라이브 포인트 후에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 전에 발생하는 광고를 해결할지 여부를 결정할 수 있습니다.

사용자가 DVR 스트림 시작 시 컨텐츠를 보기 시작하면 TVSDK는 해당 시간에 스트림에 대한 모든 광고를 확인합니다. 그러나 사용자가 스트림 시작 후 어느 시점에서 컨텐츠를 보기 시작할 때 사용자의 현재 라이브 포인트 뒤에 발생하는 광고만 해결할지 또는 현재 라이브 포인트 전에 발생한 광고를 해결할지 여부를 결정할 수 있습니다.

>[!TIP]
>
>현재 라이브 포인트 후에 광고를 해결하는 것이 더 빠르지만 사용자가 뒤로 검색하는 경우 이 옵션은 플레이어가 이전에 표시된 광고를 재생하지 못하도록 합니다.

## DVR 창에 대한 제어 및 로드 {#section_2D93E2E947644D66B6F6ED1DD6742C25}

DVR 창에 대한 광고 로드를 제어하려면

전체 스트림에 대한 모든 광고를 로드하려면 `PTAdMetadata.enableDVRAds` 속성 대상 `YES`.

>[!NOTE]
>
>기본값은 입니다. `NO`, 그리고 이 옵션은 현재 라이브 포인트에서 광고만 로드합니다.

For example:

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

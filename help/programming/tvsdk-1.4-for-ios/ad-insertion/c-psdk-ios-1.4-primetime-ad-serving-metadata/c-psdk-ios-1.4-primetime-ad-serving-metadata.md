---
description: TVSDK는 VOD 및 라이브/선형 스트림에 대한 광고 해결 및 삽입을 지원합니다.
title: Primetime 광고 서버 메타데이터
exl-id: 3723dd2f-292c-4ce5-9670-fda1b1f2b5df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# 개요 {#primetime-ad-server-metadata-overview}

TVSDK는 VOD 및 라이브/선형 스트림에 대한 광고 해결 및 삽입을 지원합니다.

>[!NOTE]
>
>비디오 콘텐츠에 광고를 포함하려면 먼저 다음 메타데이터 정보를 제공하십시오.
>
>* A `mediaID`: 재생할 특정 콘텐츠를 식별합니다.
>* 사용자 `zoneID`회사 또는 웹 사이트를 식별합니다.
>* 할당된 광고 서버의 도메인을 지정하는 광고 서버 도메인.
>* 기타 타깃팅 매개 변수.
>


## Primetime 광고 서버 메타데이터 설정 {#section_86C4A3B2DF124770B9B7FD2511394313}

애플리케이션이 TVSDK에 필요한 을 제공해야 합니다. `PTAuditudeMetadata` 광고 서버에 연결하기 위한 정보입니다.

광고 서버 메타데이터를 설정하려면 다음을 수행하십시오.

1. 의 인스턴스 만들기 [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) 속성을 설정합니다.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 설정 `PTAuditudeMetadata` 인스턴스를 현재 메타데이터로 사용 `PTMediaPlayerItem` 를 사용한 메타데이터 `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   예를 들면 다음과 같습니다.

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```

## 전체 이벤트 재생에서 광고 활성화 {#section_6016E1DAF03645C8A8388D03C6AB7571}

FER(전체 이벤트 재생)은 라이브/DVR 에셋 역할을 하는 VOD 에셋이므로, 애플리케이션이 광고를 올바르게 배치할 수 있도록 조치를 취해야 합니다.

라이브 콘텐츠의 경우, TVSDK는 매니페스트의 메타데이터/큐를 사용하여 광고를 배치할 위치를 결정합니다. 그러나 때로는 라이브/선형 콘텐츠가 VOD 콘텐츠와 유사할 수 있습니다. 예를 들어 라이브 컨텐츠가 완료되면 `EXT-X-ENDLIST` 태그가 라이브 매니페스트에 추가됩니다. HLS의 경우 `EXT-X-ENDLIST` 태그는 스트림이 VOD 스트림임을 의미합니다. TVSDK는 광고를 올바르게 삽입하기 위해 이 스트림을 일반 VOD 스트림과 자동으로 구분할 수 없습니다.

애플리케이션은 를 지정하여 콘텐츠가 라이브인지 VOD인지를 TVSDK에 알려주어야 합니다. `PTAdSignalingMode`.

FER 스트림의 경우, Adobe Primetime Ad Decisioning 서버는 재생을 시작하기 전에 타임라인에 삽입해야 하는 광고 브레이크 목록을 제공해서는 안 됩니다. 이는 VOD 콘텐츠의 일반적인 프로세스입니다. 대신, 다른 시그널링 모드를 지정하면 TVSDK가 FER 매니페스트에서 모든 큐 포인트를 읽고 각 큐 포인트에 대해 광고 서버로 이동하여 광고 브레이크를 요청합니다. 이 프로세스는 라이브/DVR 콘텐츠와 유사합니다.

큐 포인트와 연결된 각 요청 외에도 TVSDK는 프리롤 광고에 대한 추가 광고 요청을 만듭니다.

1. vCMS와 같은 외부 소스에서 사용해야 하는 신호 모드를 가져옵니다.
1. 광고 관련 메타데이터를 만듭니다.
1. 기본 동작을 덮어써야 하는 경우 `PTAdSignalingMode` 를 사용하여 `PTAdMetadata.signalingMode`.

   유효한 값은 다음과 같습니다. `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`, 및 `PTAdSignalingModeServerMap`.

   호출하기 전에 광고 신호 모드를 설정해야 합니다. `prepareToPlay`. TVSDK가 타임라인에서 광고를 확인하고 배치하면 광고 신호 모드에 대한 변경 사항이 무시됩니다. 리소스에 대한 광고 메타데이터를 만들 때 모드를 설정합니다.

1. 계속 재생합니다.

   ```
      PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.zoneId = your-auditude-zone-id; 
   adMetadata.domain = @"your-auditude-domain"; 
   //adMetadata.enableDVRAds = YES; // FOR LIVE DVR case 
   //adMetadata.signalingMode = PTAdSignalingModeManifestCues;  
   // FOR VOD FER case 
   NSMutableDictionary *targetingParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [targetingParameters setValue:@"ipad" forKey:@"device"]; 
   [targetingParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.targetingParameters = targetingParameters; 
   NSMutableDictionary *customParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [customParameters setValue:@"your-media-id" forKey:@"NW_ID"]; 
   [customParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.customParameters = customParameters; 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   ```

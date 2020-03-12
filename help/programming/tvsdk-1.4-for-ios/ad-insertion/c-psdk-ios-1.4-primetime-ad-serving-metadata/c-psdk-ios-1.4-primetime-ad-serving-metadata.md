---
description: TVSDK는 VOD 및 라이브/리니어 스트림에 대한 광고 해결 및 삽입을 지원합니다.
seo-description: TVSDK는 VOD 및 라이브/리니어 스트림에 대한 광고 해결 및 삽입을 지원합니다.
seo-title: Primetime 광고 서버 메타데이터
title: Primetime 광고 서버 메타데이터
uuid: 314f14c0-4da4-4da6-96f9-5a5ffea22a99
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 개요 {#primetime-ad-server-metadata-overview}

TVSDK는 VOD 및 라이브/리니어 스트림에 대한 광고 해결 및 삽입을 지원합니다.

>[!NOTE] {othertype=&quot;Prequisite&quot;}
>
>비디오 컨텐츠에 광고를 포함하려면 먼저 다음 메타데이터 정보를 제공합니다.
>
>* 재생할 특정 컨텐츠를 식별하는 `mediaID`A.
>* 회사 또는 웹 사이트를 식별하는 `zoneID`사용자.
>* 지정된 광고 서버의 도메인을 지정하는 광고 서버 도메인.
>* 기타 타깃팅 매개 변수.
>



## Primetime 광고 서버 메타데이터 설정 {#section_86C4A3B2DF124770B9B7FD2511394313}

응용 프로그램은 광고 서버에 연결하기 위해 필요한 `PTAuditudeMetadata` 정보를 TVSDK에 제공해야 합니다.

광고 서버 메타데이터를 설정하려면

1. PTAuditudeMetadata의 인스턴스를 [만들고](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) 해당 속성을 설정합니다.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 을 사용하여 `PTAuditudeMetadata` 인스턴스를 현재 `PTMediaPlayerItem` 메타데이터에 대한 메타데이터로 설정합니다 `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   다음은 예입니다.

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

FER(Full-Event Replay)는 실시간/DVR 자산 역할을 하는 VOD 자산이므로 애플리케이션이 광고가 올바르게 배치되도록 조치를 취해야 합니다.

라이브 콘텐츠의 경우 TVSDK는 매니페스트의 메타데이터/큐를 사용하여 광고를 배치할 위치를 결정합니다. 그러나 실시간/선형 컨텐츠는 VOD 컨텐츠와 유사할 수 있습니다. 예를 들어 라이브 컨텐츠가 완료되면 `EXT-X-ENDLIST` 태그가 라이브 매니페스트에 추가됩니다. HLS의 경우 `EXT-X-ENDLIST` 태그는 스트림이 VOD 스트림임을 의미합니다. TVSDK는 이 스트림을 일반 VOD 스트림과 자동으로 구별하여 광고를 올바로 삽입할 수 없습니다.

애플리케이션은 컨텐츠를 지정하여 TVSDK에 컨텐츠의 실시간 또는 VOD를 알려주어야 `PTAdSignalingMode`합니다.

FER 스트림의 경우 Adobe Primetime 광고 결정 서버는 재생을 시작하기 전에 타임라인에 삽입해야 하는 광고 중단 목록을 제공하지 않아야 합니다. VOD 컨텐츠의 일반적인 프로세스입니다. 대신 다른 신호 모드를 지정하여 TVSDK는 FER 매니페스트에서 모든 큐 포인트를 읽고 각 큐 포인트에 대한 광고 서버로 이동하여 광고 중단을 요청합니다. 이 프로세스는 라이브/DVR 컨텐츠와 유사합니다.

TVSDK는 큐 포인트와 연결된 각 요청 외에도 프리롤 광고에 대한 추가 광고 요청을 수행합니다.

1. vCMS와 같은 외부 소스에서 사용해야 하는 신호 모드를 얻습니다.
1. 광고 관련 메타데이터를 만듭니다.
1. 기본 동작을 덮어써야 하는 경우 를 `PTAdSignalingMode` 사용하여 지정합니다 `PTAdMetadata.signalingMode`.

   유효한 값은 `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`및 `PTAdSignalingModeServerMap`입니다.

   호출하기 전에 광고 신호 모드를 설정해야 합니다 `prepareToPlay`. TVSDK가 타임라인에서 광고를 확인하고 배치하기 시작하면 광고 신호 모드로 변경된 내용은 무시됩니다. 리소스에 대한 광고 메타데이터를 만들 때 모드를 설정합니다.

1. 계속 재생할 수 있습니다.

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


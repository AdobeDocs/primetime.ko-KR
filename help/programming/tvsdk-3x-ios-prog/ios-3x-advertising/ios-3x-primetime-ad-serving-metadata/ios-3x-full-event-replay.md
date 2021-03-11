---
description: TVSDK는 VOD 및 라이브/리니어 스트림에 대한 광고 해결 및 삽입을 지원합니다.
title: Primetime 광고 서버 메타데이터
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# 전체 이벤트 재생 {#section_6016E1DAF03645C8A8388D03C6AB7571}에서 광고 활성화

FER(Full-Event Replay)는 실시간/DVR 자산 역할을 하는 VOD 자산이므로 애플리케이션이 광고를 올바로 배치하도록 조치를 취해야 합니다.

라이브 콘텐츠의 경우 TVSDK는 매니페스트의 메타데이터/큐를 사용하여 광고를 배치할 위치를 결정합니다. 하지만 실시간/선형 컨텐츠가 VOD 컨텐츠와 비슷할 수도 있습니다. 예를 들어 라이브 콘텐츠가 완료되면 `EXT-X-ENDLIST` 태그가 라이브 매니페스트에 추가됩니다. HLS의 경우 `EXT-X-ENDLIST` 태그는 스트림이 VOD 스트림임을 의미합니다. TVSDK는 광고를 올바로 삽입하기 위해 일반 VOD 스트림과 이 스트림을 자동으로 구별할 수 없습니다.

응용 프로그램은 `PTAdSignalingMode`을(를) 지정하여 컨텐츠가 실시간 또는 VOD인지 TVSDK에 알려주어야 합니다.

FER 스트림의 경우 Adobe Primetime 광고 결정 서버는 재생을 시작하기 전에 타임라인에 삽입해야 하는 광고 중단 목록을 제공하지 않아야 합니다. VOD 컨텐츠의 일반적인 프로세스입니다. 대신 다른 신호 모드를 지정하여 TVSDK는 FER 매니페스트에서 모든 큐 포인트를 읽고 각 큐 포인트의 광고 서버로 이동하여 광고 중단을 요청합니다. 이 프로세스는 라이브/DVR 컨텐츠와 유사합니다.

TVSDK는 큐 포인트와 연관된 각 요청 이외에도 프리롤 광고에 대한 추가 광고 요청을 수행합니다.

1. vCMS와 같은 외부 소스에서 사용해야 하는 신호 모드를 가져옵니다.
1. 광고 관련 메타데이터를 만듭니다.
1. 기본 동작을 덮어써야 하는 경우 `PTAdMetadata.signalingMode`을(를) 사용하여 `PTAdSignalingMode`을(를) 지정합니다.

   유효한 값은 `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues` 및 `PTAdSignalingModeServerMap`입니다.

   `prepareToPlay`을(를) 호출하기 전에 광고 신호 모드를 설정해야 합니다. TVSDK가 타임라인에서 광고를 확인하고 배치하기 시작하면 광고 신호 모드에 대한 변경 사항은 무시됩니다. 리소스에 대한 광고 메타데이터를 만들 때 모드를 설정합니다.

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

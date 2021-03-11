---
description: TVSDK는 VOD 및 라이브/리니어 스트림에 대한 광고 해결 및 삽입을 지원합니다.
title: Primetime 광고 서버 메타데이터
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 개요 {#primetime-ad-server-metadata-overview}

TVSDK는 VOD 및 라이브/리니어 스트림에 대한 광고 해결 및 삽입을 지원합니다.

## 사전 요구 사항

비디오 컨텐츠에 광고를 포함하려면 먼저 다음 메타데이터 정보를 제공합니다.

* 재생할 특정 컨텐츠를 식별하는 `mediaID`
* 회사 또는 웹 사이트를 식별하는 `zoneID`.
* 할당된 광고 서버의 도메인을 지정하는 광고 서버 도메인입니다.
* 기타 타깃팅 매개 변수.

## Primetime 광고 서버 메타데이터 {#section_86C4A3B2DF124770B9B7FD2511394313} 설정

광고 서버에 연결하려면 응용 프로그램에서 필요한 `PTAuditudeMetadata` 정보를 TVSDK에 제공해야 합니다.

광고 서버 메타데이터를 설정하려면

1. [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html)의 인스턴스를 만들고 해당 속성을 설정합니다.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. `PTAdResolvingMetadataKey`을(를) 사용하여 현재 `PTMediaPlayerItem` 메타데이터의 메타데이터로 `PTAuditudeMetadata` 인스턴스를 설정합니다.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   다음은 한 예입니다.

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

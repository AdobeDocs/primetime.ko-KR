---
description: TVSDK는 VOD 및 라이브/선형 스트림에 대한 광고 해결 및 삽입을 지원합니다.
title: Primetime 광고 서버 메타데이터
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 개요 {#primetime-ad-server-metadata-overview}

TVSDK는 VOD 및 라이브/선형 스트림에 대한 광고 해결 및 삽입을 지원합니다.

## 전제 조건

비디오 콘텐츠에 광고를 포함하려면 먼저 다음 메타데이터 정보를 제공하십시오.

* A `mediaID`: 재생할 특정 콘텐츠를 식별합니다.
* 사용자 `zoneID`회사 또는 웹 사이트를 식별합니다.
* 할당된 광고 서버의 도메인을 지정하는 광고 서버 도메인.
* 기타 타깃팅 매개 변수.

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

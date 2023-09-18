---
description: Ad Resolver가 작동할 수 있도록 하려면 Adobe Primetime ad decisioning과 같은 광고 공급자는 공급자에 대한 연결을 활성화하기 위한 구성 값이 필요합니다.
title: 광고 삽입 메타데이터
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 광고 삽입 메타데이터 {#ad-insertion-metadata}

Ad Resolver가 작동할 수 있도록 하려면 Adobe Primetime ad decisioning과 같은 광고 공급자는 공급자에 대한 연결을 활성화하기 위한 구성 값이 필요합니다.

TVSDK에는 Primetime ad decisioning 라이브러리가 포함됩니다. Primetime ad decisioning 서버의 광고를 포함하는 콘텐츠에 대해 애플리케이션이 다음 필수 사항을 제공해야 합니다 `AuditudeSettings` 정보:

* `mediaID`: 재생할 비디오의 고유 식별자입니다.

  게시자는 Adobe Primetime 광고 결정 서버에 비디오 콘텐츠 및 광고 정보를 제출할 때 mediaID를 지정합니다. 이 ID는 Primetime ad decisioning에서 서버에서 비디오에 대한 관련 광고 정보를 검색하는 데 사용됩니다.

* 사용자 `zoneID`는 Adobe에 의해 할당되며 회사 또는 웹 사이트를 식별합니다.
* 할당된 광고 서버의 도메인입니다.
* 기타 타깃팅 매개 변수.

  필요에 따라 광고 공급자의 필요에 따라 이러한 매개 변수를 포함할 수 있습니다.

## 광고 삽입 메타데이터 설정 {#set-up-ad-insertion-metadata}

MetadataNode 클래스를 확장하는 도우미 클래스 AuditudeSettings 를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>이전에 Adobe Primetime ad decisioning을 Auditude라고 했습니다.

광고 메타데이터는에 있습니다. `MediaResource.metadata` 속성. 새 비디오 재생을 시작할 때 애플리케이션은 올바른 광고 메타데이터 설정을 담당합니다.

1. 빌드 `AuditudeSettings` 인스턴스.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Adobe Primetime ad decisioning mediaID, zoneID, 도메인 및 선택적 타깃팅 매개 변수를 설정합니다.

   ```
   auditudeSettings.zoneId = "yourZoneID"; 
   auditudeSettings.mediaId = "media_identifier"; 
   auditudeSettings.domain = "yourAuditudeDomain"; 
   var targetingInfo:Metadata = new Metadata(); 
   targetingInfo.setValue("yourParamName", "yourParamValue"); 
   auditudeSettings.targetingInfo = targetingInfo;
   ```

   >[!TIP]
   >
   >미디어 ID는 TVSDK에서 md5 값으로 변환되는 문자열로 사용되며 `u` Primetime ad decisioning URL 요청의 값입니다. 예:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 만들기 `MediaResource` 미디어 스트림 URL과 이전에 만든 광고 메타데이터를 사용하는 인스턴스.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. 을(를) 로드합니다 `MediaResource` 을 통해 개체 `MediaPlayer.replaceCurrentResource` 메서드를 사용합니다.

   다음 `MediaPlayer` 미디어 스트림 매니페스트 로드 및 처리를 시작합니다.

1. (선택 사항) `MediaPlayerItem` 대체 오디오 트랙이 있는지 또는 스트림이 보호되는지 여부에 관계없이 스트림이 라이브되는지 여부를 확인하는 인스턴스입니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 될 수 있습니다. 예를 들어, 오디오 트랙이 두 개인 경우 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 호출 `MediaPlayer.prepareToPlay` 광고 워크플로우를 시작합니다.

   광고가 해결되고 타임라인에 배치되면 `MediaPlayer` 준비된 상태로 전환합니다.
1. 호출 `MediaPlayer.play` 재생을 시작합니다.

이제 TVSDK에 미디어가 재생될 때 광고가 포함됩니다.

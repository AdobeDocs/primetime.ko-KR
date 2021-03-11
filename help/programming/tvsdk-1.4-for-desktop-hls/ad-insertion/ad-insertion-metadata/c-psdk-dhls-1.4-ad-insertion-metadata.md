---
description: 광고 확인자가 작동하도록 허용하려면, Adobe Primetime 광고 결정 등의 광고 제공자는 공급자에 대한 연결을 활성화할 수 있도록 구성 값이 필요합니다.
title: 광고 삽입 메타데이터
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# 광고 삽입 메타데이터 {#ad-insertion-metadata}

광고 확인자가 작동하도록 허용하려면, Adobe Primetime 광고 결정 등의 광고 제공자는 공급자에 대한 연결을 활성화할 수 있도록 구성 값이 필요합니다.

TVSDK에는 Primetime 광고 결정 라이브러리가 포함되어 있습니다. 콘텐츠가 Primetime 광고 결정 서버의 광고를 포함하려면 다음 필수 `AuditudeSettings` 정보를 제공해야 합니다.

* `mediaID`를 반환합니다. 이것은 재생할 비디오에 대한 고유 식별자입니다.

   발행자는 비디오 컨텐츠 및 광고 정보를 Adobe Primetime 광고 결정 서버에 제출할 때 mediaID를 할당합니다. 이 ID는 Primetime 광고 결정 기능이 서버에서 비디오에 대한 관련 광고 정보를 검색하는 데 사용됩니다.

* Adobe에 의해 할당된 `zoneID`은 귀사 또는 웹 사이트를 식별합니다.
* 할당된 광고 서버의 도메인.
* 기타 타깃팅 매개 변수.

   광고 공급자의 필요성과 요구에 따라 이러한 매개 변수를 포함할 수 있습니다.

## 광고 삽입 메타데이터 설정 {#set-up-ad-insertion-metadata}

MetadataNode 클래스를 확장하는 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>Adobe Primetime 광고 의사 결정은 이전에 Auditude라고 알려져 있었습니다.

광고 메타데이터는 `MediaResource.metadata` 속성에 있습니다. 새 비디오 재생을 시작할 때 애플리케이션에서 올바른 광고 메타데이터를 설정할 책임이 있습니다.

1. `AuditudeSettings` 인스턴스를 만듭니다.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Adobe Primetime 광고 결정 미디어 ID, zoneID, 도메인 및 선택적 타깃팅 매개 변수를 설정합니다.

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
   >미디어 ID는 TVSDK에서 문자열로 소비되고, md5 값으로 변환되며, Primetime 광고 결정 URL 요청의 `u` 값에 사용됩니다. 예:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 미디어 스트림 URL 및 이전에 만든 광고 메타데이터를 사용하여 `MediaResource` 인스턴스를 만듭니다.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. `MediaPlayer.replaceCurrentResource` 메서드를 통해 `MediaResource` 개체를 로드합니다.

   `MediaPlayer`은 미디어 스트림 매니페스트를 로드하고 처리하기 시작합니다.

1. (선택 사항) 대체 오디오 트랙이 있는지 또는 스트림이 보호되어 있는지 여부에 관계없이 `MediaPlayerItem` 인스턴스를 쿼리하여 스트림이 라이브인지 확인합니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 될 수 있습니다. 예를 들어 두 개의 오디오 트랙이 있는 것으로 알고 있는 경우 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 광고 워크플로우를 시작하려면 `MediaPlayer.prepareToPlay`을(를) 호출합니다.

   광고를 확인하고 타임라인에 배치하면 `MediaPlayer` 은 준비된 상태로 전환됩니다.
1. 재생을 시작하려면 `MediaPlayer.play`을(를) 호출합니다.

이제 미디어가 재생될 때 TVSDK에 광고가 포함됩니다.
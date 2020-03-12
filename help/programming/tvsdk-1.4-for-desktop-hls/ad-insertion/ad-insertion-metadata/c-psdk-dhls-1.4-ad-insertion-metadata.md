---
description: 광고 확인자가 작동하도록 허용하려면 Adobe Primetime 광고 결정 등의 광고 제공업체는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.
seo-description: 광고 확인자가 작동하도록 허용하려면 Adobe Primetime 광고 결정 등의 광고 제공업체는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.
seo-title: 광고 삽입 메타데이터
title: 광고 삽입 메타데이터
uuid: 3eb024c3-4bb5-4bee-943e-fe0c60379e60
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 광고 삽입 메타데이터 {#ad-insertion-metadata}

광고 확인자가 작동하도록 허용하려면 Adobe Primetime 광고 결정 등의 광고 제공업체는 공급자에 대한 연결을 활성화하려면 구성 값이 필요합니다.

TVSDK에는 Primetime 광고 결정 라이브러리가 포함되어 있습니다. 콘텐츠가 Primetime 광고 결정 서버의 광고를 포함하려면 다음 필수 `AuditudeSettings` 정보를 응용 프로그램에 제공해야 합니다.

* `mediaID`에 표시되는 값은 재생할 비디오의 고유 식별자입니다.

   발행자는 비디오 컨텐츠 및 광고 정보를 Adobe Primetime 광고 결정 서버에 제출할 때 mediaID를 할당합니다. 이 ID는 Primetime 광고 결정 시 서버에서 비디오에 대한 관련 광고 정보를 검색하는 데 사용됩니다.

* Adobe `zoneID`가 지정하는 사용자의 회사 또는 웹 사이트를 확인합니다.
* 할당된 광고 서버의 도메인.
* 기타 타깃팅 매개 변수.

   광고 공급자의 요구 사항과 요구 사항에 따라 이러한 매개 변수를 포함할 수 있습니다.

## 광고 삽입 메타데이터 설정 {#set-up-ad-insertion-metadata}

MetadataNode 클래스를 확장하는 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>Adobe Primetime 광고 의사 결정은 이전에 Auditude라고 불렸습니다.

광고 메타데이터는 `MediaResource.metadata` 속성에 있습니다. 새 비디오 재생을 시작할 때 애플리케이션에서 올바른 광고 메타데이터를 설정해야 합니다.

1. 인스턴스를 `AuditudeSettings` 만듭니다.

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
   >미디어 ID는 TVSDK에서 문자열로 사용되며, 이는 md5 값으로 변환되며 Primetime 광고 결정 URL 요청의 `u` 값에 사용됩니다. 예:
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

1. 메서드를 통해 `MediaResource` 개체를 `MediaPlayer.replaceCurrentResource` 로드합니다.

   미디어 스트림 매니페스트의 로드 및 처리가 `MediaPlayer` 시작됩니다.

1. (선택 사항) `MediaPlayerItem` 인스턴스를 쿼리하여 대체 오디오 트랙이 있는지 또는 스트림이 보호되는지 여부에 관계없이 스트림이 라이브인지 확인합니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 될 수 있습니다. 예를 들어 두 개의 오디오 트랙이 있는 경우 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 광고 워크플로우를 `MediaPlayer.prepareToPlay` 시작하려면 전화 주십시오.

   광고가 해결되고 타임라인에 배치되면 준비된 상태로 `MediaPlayer` 전환됩니다.
1. 재생을 `MediaPlayer.play` 시작하려면 전화 걸기

이제 TVSDK에 미디어가 재생될 때 광고가 포함됩니다.
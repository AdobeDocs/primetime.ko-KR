---
description: MetadataNode 클래스를 확장하는 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.
title: 광고 삽입 메타데이터 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 광고 삽입 메타데이터 설정 {#set-up-ad-insertion-metadata}

`MetadataNode` 클래스를 확장하는 도우미 클래스 `AuditudeSettings`을 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>Adobe Primetime 광고 의사 결정은 이전에 Auditude라고 알려져 있었습니다.

광고 메타데이터는 `MediaResource.Metadata` 속성에 있습니다. 새 비디오 재생을 시작할 때 애플리케이션에서 올바른 광고 메타데이터를 설정할 책임이 있습니다.

1. `AuditudeSettings` 인스턴스를 만듭니다.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Adobe Primetime 광고 의사 결정 `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>` 및 선택적 타깃팅 매개 변수를 설정합니다.

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
   
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
   
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >미디어 ID는 TVSDK에서 문자열로 소비되고, md5 값으로 변환되며, Primetime 광고 결정 URL 요청의 `u` 값에 사용됩니다. 예:
   >
   >`https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 미디어 스트림 URL 및 이전에 만든 광고 메타데이터를 사용하여 `MediaResource` 인스턴스를 만듭니다.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. `MediaPlayer.replaceCurrentResource` 메서드를 통해 `MediaResource` 개체를 로드합니다.

   `MediaPlayer`은 미디어 스트림 매니페스트를 로드하고 처리하기 시작합니다.

1. `MediaPlayer`이(가) INITIALIZED 상태로 전환되면 `MediaPlayer.CurrentItem` 메서드를 통해 `MediaPlayerItem` 인스턴스 형태로 미디어 스트림 특성을 가져옵니다.
1. (선택 사항) 대체 오디오 트랙이 있는지 또는 스트림이 보호되어 있는지 여부와 관계없이 `MediaPlayerItem` 인스턴스를 쿼리하여 스트림이 라이브인지 확인합니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 될 수 있습니다. 예를 들어 두 개의 오디오 트랙이 있는 것으로 알고 있는 경우 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 광고 워크플로우를 시작하려면 `MediaPlayer.prepareToPlay`을(를) 호출합니다.

   광고를 확인하고 타임라인에 배치하면 `MediaPlayer`은 `PREPARED` 상태로 전환됩니다.
1. 재생을 시작하려면 `MediaPlayer.play`을(를) 호출합니다.
이제 미디어가 재생될 때 TVSDK에 광고가 포함됩니다.

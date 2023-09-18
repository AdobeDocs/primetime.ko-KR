---
description: MetadataNode 클래스를 확장하는 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.
title: 광고 삽입 메타데이터 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 광고 삽입 메타데이터 설정 {#set-up-ad-insertion-metadata}

MetadataNode 클래스를 확장하는 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>이전에 Adobe Primetime ad decisioning을 Auditude라고 했습니다.

광고 메타데이터는에 있습니다. `MediaResource.Metadata` 속성. 새 비디오 재생을 시작할 때 애플리케이션은 올바른 광고 메타데이터 설정을 담당합니다.

1. 빌드 `AuditudeSettings` 인스턴스.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Adobe Primetime 광고 결정 설정 `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>`및 선택적 타깃팅 매개 변수

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
   >미디어 ID는 TVSDK에서 md5 값으로 변환되는 문자열로 사용되며 `u` Primetime ad decisioning URL 요청의 값입니다. 예:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 만들기 `MediaResource` 미디어 스트림 URL과 이전에 만든 광고 메타데이터를 사용하는 인스턴스.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 을(를) 로드합니다 `MediaResource` 을 통해 개체 `MediaPlayer.replaceCurrentResource` 메서드를 사용합니다.

   다음 `MediaPlayer` 미디어 스트림 매니페스트 로드 및 처리를 시작합니다.

1. 다음의 경우 `MediaPlayer` 초기화된 상태로 전환하면 미디어 스트림 특성을 `MediaPlayerItem` 인스턴스를 통해 `MediaPlayer.CurrentItem` 메서드를 사용합니다.
1. (선택 사항) `MediaPlayerItem` 대체 오디오 트랙이 있는지 또는 스트림이 보호되는지 여부에 관계없이 스트림이 라이브되는지 여부를 확인하는 인스턴스입니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 될 수 있습니다. 예를 들어, 오디오 트랙이 두 개인 경우 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 호출 `MediaPlayer.prepareToPlay` 광고 워크플로우를 시작합니다.

   광고가 해결되고 타임라인에 배치되면 `MediaPlayer` 로 전환 `PREPARED` 주.
1. 호출 `MediaPlayer.play` 재생을 시작합니다.

이제 TVSDK에 미디어가 재생될 때 광고가 포함됩니다.

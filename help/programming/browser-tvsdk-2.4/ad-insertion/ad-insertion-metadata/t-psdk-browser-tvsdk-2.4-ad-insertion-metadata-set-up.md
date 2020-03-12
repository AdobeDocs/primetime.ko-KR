---
description: 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.
seo-description: 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.
seo-title: 광고 삽입 메타데이터 설정
title: 광고 삽입 메타데이터 설정
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 광고 삽입 메타데이터 설정{#set-up-ad-insertion-metadata}

도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>Adobe Primetime 광고 의사 결정은 이전에는 Auditude라고 불렀습니다.

1. 인스턴스를 `AuditudeSettings` 만듭니다.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Adobe Primetime 광고 결정 미디어 ID, zoneID, 도메인 및 선택적 타깃팅 매개 변수를 설정합니다.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 미디어 스트림 URL 및 이전에 만든 광고 메타데이터를 사용하여 `MediaResource` 인스턴스를 만듭니다.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 메서드를 통해 `MediaResource` 개체를 `MediaPlayer.replaceCurrentResource(resource)` 로드합니다.

   미디어 스트림 매니페스트의 로드 및 처리가 `MediaPlayer` 시작됩니다.

1. INITIALIZED `MediaPlayer` 상태로 전환하면 속성을 통해 `MediaPlayerItem` 인스턴스의 형태로 미디어 스트림 특성을 가져옵니다 `MediaPlayer.CurrentItem` .
1. (선택 사항) `MediaPlayerItem` 인스턴스를 쿼리하여 대체 오디오 트랙이 있는지 여부와 상관없이 스트림이 라이브인지 확인합니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 될 수 있습니다. 예를 들어 두 개의 오디오 트랙이 있는 경우 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 광고 워크플로우를 `MediaPlayer.prepareToPlay` 시작하려면 전화 주십시오.

   광고가 해결되고 타임라인에 배치되면 준비된 상태로 `  MediaPlayer ` 전환됩니다.
1. 재생을 `MediaPlayer.play` 시작하려면 전화 걸기
이제 미디어 재생 시 브라우저 TVSDK에 광고가 포함됩니다.

---
description: 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.
title: 광고 삽입 메타데이터 설정
exl-id: 03b2237b-6b3b-46cf-bc0b-691513033463
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 광고 삽입 메타데이터 설정{#set-up-ad-insertion-metadata}

도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>Adobe Primetime ad decisioning을 이전에 Auditude 라고 했습니다.

1. 빌드 `AuditudeSettings` 인스턴스.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Adobe Primetime ad decisioning mediaID, zoneID, 도메인 및 선택적 타깃팅 매개 변수를 설정합니다.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 만들기 `MediaResource` 미디어 스트림 URL과 이전에 만든 광고 메타데이터를 사용하는 인스턴스.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 을(를) 로드합니다 `MediaResource` 을 통해 개체 `MediaPlayer.replaceCurrentResource(resource)` 메서드를 사용합니다.

   다음 `MediaPlayer` 미디어 스트림 매니페스트 로드 및 처리를 시작합니다.

1. 다음의 경우 `MediaPlayer` 초기화된 상태로 전환하면 미디어 스트림 특성을 `MediaPlayerItem` 인스턴스를 통해 `MediaPlayer.CurrentItem` 특성.
1. (선택 사항) `MediaPlayerItem` 대체 오디오 트랙이 있는지 여부에 관계없이 스트림이 라이브인지 여부를 확인할 수 있는 인스턴스입니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 될 수 있습니다. 예를 들어, 오디오 트랙이 두 개인 경우 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 호출 `MediaPlayer.prepareToPlay` 광고 워크플로우를 시작합니다.

   광고가 해결되고 타임라인에 배치되면 `  MediaPlayer ` 준비된 상태로 전환합니다.
1. 호출 `MediaPlayer.play` 재생을 시작합니다.
이제 미디어가 재생될 때 브라우저 TVSDK에 광고가 포함됩니다.

---
description: 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.
seo-description: 도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.
seo-title: 광고 삽입 메타데이터 설정
title: 광고 삽입 메타데이터 설정
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 광고 삽입 메타데이터 설정{#set-up-ad-insertion-metadata}

도우미 클래스 AuditudeSettings를 사용하여 Adobe Primetime 광고 결정 메타데이터를 설정합니다.

>[!TIP]
>
>Adobe Primetime 광고 의사 결정은 이전에 Auditude로 알려져 있었습니다.

1. `AuditudeSettings` 인스턴스를 만듭니다.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Adobe Primetime 광고 결정 mediaID, zoneID, 도메인 및 선택적 타깃팅 매개 변수를 설정합니다.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 미디어 스트림 URL과 이전에 만든 광고 메타데이터를 사용하여 `MediaResource` 인스턴스를 만듭니다.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. `MediaPlayer.replaceCurrentResource(resource)` 메서드를 통해 `MediaResource` 개체를 로드합니다.

   `MediaPlayer`은 미디어 스트림 매니페스트를 로드하고 처리하기 시작합니다.

1. `MediaPlayer`이(가) INITIALIZED 상태로 전환되면 미디어 스트림 특성을 `MediaPlayer.CurrentItem` 속성을 통해 `MediaPlayerItem` 인스턴스의 형태로 가져옵니다.
1. (선택 사항) 대체 오디오 트랙이 있는지 여부에 관계없이 `MediaPlayerItem` 인스턴스를 쿼리하여 스트림이 라이브인지 확인합니다.

   이 정보는 재생을 위한 UI를 준비하는 데 도움이 됩니다. 예를 들어 두 개의 오디오 트랙이 있다는 것을 알고 있다면 이러한 트랙 간에 전환하는 UI 컨트롤을 포함할 수 있습니다.

1. 광고 워크플로우를 시작하려면 `MediaPlayer.prepareToPlay`을(를) 호출합니다.

   광고가 해결되고 타임라인에 배치되면 `  MediaPlayer ` 은 준비된 상태로 전환됩니다.
1. 재생을 시작하려면 `MediaPlayer.play`을(를) 호출합니다.
이제 미디어 재생 시 브라우저 TVSDK에 광고가 포함됩니다.

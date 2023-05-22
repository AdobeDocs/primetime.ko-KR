---
description: MediaPlayer 인터페이스는 미디어 플레이어의 기능 및 동작을 캡슐화합니다.
title: MediaPlayer 설정
exl-id: eec51f3e-4779-4fb5-b735-d5be412de64e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# MediaPlayer 설정 {#set-up-the-mediaplayer}

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 만드는 도구를 제공합니다.

플랫폼의 도구를 사용하여 플레이어를 만들고 TVSDK의 미디어 플레이어 보기에 연결하십시오. 이 보기에는 비디오를 재생하고 관리하는 메서드가 있습니다. 예를 들어 TVSDK는 재생 및 일시 중지 메서드를 제공합니다. 플랫폼에서 사용자 인터페이스 단추를 만들고 이러한 TVSDK 메서드를 호출하도록 단추를 설정할 수 있습니다.MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.

TVSDK는 `MediaPlayer` 인터페이스: DefaultMediaPlayer 클래스입니다. 비디오 재생 기능이 필요한 경우 를 인스턴스화합니다. `DefaultMediaPlayer`.

>[!NOTE]
>
>와 상호 작용 `DefaultMediaPlayer` 에 의해 노출된 메서드만 있는 인스턴스 `MediaPlayer` 인터페이스.

1. 인스턴스화 `MediaPlayerContext` application-loaded 사용 `authorizedFeatures` 인스턴스(참조) [서명된 토큰 로드](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 인스턴스화 `MediaPlayer` public create factory 메서드 사용 `MediaPlayerContext` 컨텍스트 개체:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   제네릭을 반환합니다 `MediaPlayer` 인터페이스. 1. 인스턴스화 `MediaPlayerView` 사용할 StageVideo 인스턴스를 지정합니다.

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 연결 `MediaPlayerView` 새로 만든 보기가 있는 인스턴스:

   ```
   mediaPlayer.view = view;
   ```

1. 배치 `MediaPlayerView` 디바이스의 화면에 있는 인스턴스:

   ```
   container.addChild(view)
   ```

다음 `MediaPlayer` 이제 인스턴스를 사용할 수 있으며 장치 화면에 비디오 콘텐츠를 표시하도록 올바르게 구성되었습니다.

---
description: MediaPlayer 인터페이스는 미디어 플레이어의 기능과 비헤이비어를 캡슐화합니다.
title: MediaPlayer 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# MediaPlayer {#set-up-the-mediaplayer} 설정

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하기 위한 툴을 제공합니다.

플랫폼의 툴을 사용하여 플레이어를 만들고 TVSDK의 미디어 플레이어 보기에 연결하여 비디오를 재생하고 관리하는 방법을 살펴봅니다. 예를 들어 TVSDK는 재생 및 일시 정지 메서드를 제공합니다. 플랫폼에서 유저 인터페이스 버튼을 만들고 해당 TVSDK 메서드를 호출할 버튼을 설정할 수 있습니다. MediaPlayer 인터페이스는 미디어 플레이어의 기능과 비헤이비어를 캡슐화합니다.

TVSDK는 `MediaPlayer` 인터페이스의 단일 구현을 제공합니다.DefaultMediaPlayer 클래스입니다. 비디오 재생 기능이 필요하면 `DefaultMediaPlayer`을(를) 인스턴스화합니다.

>[!NOTE]
>
>`DefaultMediaPlayer` 인스턴스와 상호 작용하려면 `MediaPlayer` 인터페이스에서 노출되는 메서드만 사용합니다.

1. 응용 프로그램이 로드된 `authorizedFeatures` 인스턴스를 사용하여 `MediaPlayerContext`을(를) 인스턴스화합니다([서명된 토큰 로드](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md) 참조).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. `MediaPlayerContext` 컨텍스트 객체를 전달하여 public create factory 메서드를 사용하여 `MediaPlayer`을 인스턴스화합니다.

   ```
   public static function create(context:Context):MediaPlayer
   ```

   일반 `MediaPlayer` 인터페이스를 반환합니다. 1. `MediaPlayerView`을 인스턴스화하고 사용할 StageVideo 인스턴스를 지정합니다.

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. `MediaPlayerView` 인스턴스를 새로 만든 뷰와 연결합니다.

   ```
   mediaPlayer.view = view;
   ```

1. 장치의 화면에 `MediaPlayerView` 인스턴스를 배치합니다.

   ```
   container.addChild(view)
   ```

이제 `MediaPlayer` 인스턴스를 사용할 수 있으며 장치 화면에 비디오 내용을 표시하도록 올바르게 구성됩니다.
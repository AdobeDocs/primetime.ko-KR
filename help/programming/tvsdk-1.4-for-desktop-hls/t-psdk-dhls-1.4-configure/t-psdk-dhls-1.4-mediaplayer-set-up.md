---
description: MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.
seo-description: MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.
seo-title: MediaPlayer 설정
title: MediaPlayer 설정
uuid: 4b27643c-9ccd-4abb-9793-475d06ee2a88
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# MediaPlayer 설정 {#set-up-the-mediaplayer}

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하기 위한 툴을 제공합니다.

플랫폼의 툴을 사용하여 플레이어를 만들고 TVSDK의 미디어 플레이어 보기에 연결하여 비디오를 재생하고 관리하는 방법을 살펴봅니다. 예를 들어 TVSDK는 재생 및 일시 중지 메서드를 제공합니다. 플랫폼에서 유저 인터페이스 버튼을 만들고 해당 TVSDK 메서드를 호출하도록 버튼을 설정할 수 있습니다. MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.

TVSDK는 단일 `MediaPlayer` 인터페이스 구현을 제공합니다.기본 MediaPlayer 클래스입니다. 비디오 재생 기능이 필요할 경우 인스턴스화합니다 `DefaultMediaPlayer`.

>[!NOTE]
>
>인터페이스에서 노출된 메서드와만 `DefaultMediaPlayer` 인스턴스와 `MediaPlayer` 상호 작용합니다.

1. 응용 프로그램이 로드된 `MediaPlayerContext` 인스턴스를 `authorizedFeatures` 사용하여 인스턴스화합니다(서명된 토큰 [로드 참조](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 공용 팩토리 생성 방법을 `MediaPlayer` 사용하여 인스턴스화하여 `MediaPlayerContext` 컨텍스트 객체를 전달합니다.

   ```
   public static function create(context:Context):MediaPlayer
   ```

   일반 `MediaPlayer` 인터페이스를 반환합니다. 1.인스턴스화하고 사용할 StageVideo 인스턴스를 `MediaPlayerView` 지정합니다.

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 인스턴스를 새로 만든 `MediaPlayerView` 뷰와 연결합니다.

   ```
   mediaPlayer.view = view;
   ```

1. 장치의 화면에 인스턴스를 `MediaPlayerView` 배치합니다.

   ```
   container.addChild(view)
   ```

이제 `MediaPlayer` 인스턴스를 사용할 수 있으며 장치 화면에 비디오 컨텐츠를 표시하도록 올바르게 구성됩니다.
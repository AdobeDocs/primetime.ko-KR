---
description: TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하는 데 필요한 툴을 제공합니다. 또한 비디오 재생 품질을 극대화하기 위해 고안된 다양한 기능을 제공합니다.
seo-description: TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하는 데 필요한 툴을 제공합니다. 또한 비디오 재생 품질을 극대화하기 위해 고안된 다양한 기능을 제공합니다.
seo-title: 미디어 플레이어 설정
title: 미디어 플레이어 설정
uuid: 1f672484-b340-4f92-8a47-dad4c9f3b3fc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 미디어 플레이어 설정 {#set-up-the-media-player}

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하는 데 필요한 툴을 제공합니다. 또한 비디오 재생 품질을 극대화하기 위해 고안된 다양한 기능을 제공합니다.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

인스턴스를 `MediaPlayer` 인스턴스화하고 뷰를 프레임 레이아웃에 배치할 수 있습니다.

1. 인스턴스화하고 `MediaPlayer``android.content.Context` 객체를 생성자에게 전달합니다.

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 프레임 레이아웃( `android.widget.FrameLayout`)을 제공하여 `ViewGroup` 다음 `mediaPlayer`중 하나를 유지합니다.

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >다음은 만들 코드 조각입니다 `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 프레임 레이아웃 `mediaPlayer` 내부에 보기를 배치합니다.

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

   >[!NOTE]
   >
   >이제 `MediaPlayer` 인스턴스( `mediaPlayer`)를 사용할 수 있으며 장치 화면에 비디오 컨텐츠를 표시하도록 올바르게 구성됩니다.
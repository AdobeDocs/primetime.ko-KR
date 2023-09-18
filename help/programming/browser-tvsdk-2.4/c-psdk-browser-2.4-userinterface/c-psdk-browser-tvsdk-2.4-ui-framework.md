---
description: UI 프레임워크는 다양한 비디오 플레이어 관련 UI 구문을 즉시 제공하는 브라우저 TVSDK의 맨 위에 있는 UI 계층입니다. 사용자 환경에 적합한 포인트 변경을 수행하여 사용자 정의가 가능한 플레이어를 만들 수 있습니다.
title: UI 프레임워크
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# UI 프레임워크 {#the-ui-framework}

UI 프레임워크는 다양한 비디오 플레이어 관련 UI 구문을 즉시 제공하는 브라우저 TVSDK의 맨 위에 있는 UI 계층입니다. 사용자 환경에 적합한 포인트 변경을 수행하여 사용자 정의가 가능한 플레이어를 만들 수 있습니다.

>[!TIP]
>
>시각적(스키닝) 및 UI 동작은 사용자 지정할 수 있습니다.

자신의 비헤이비어를 다시 작성하거나 특정 기본 비헤이비어의 기능을 재정의할 수 있습니다. SDK와 함께 제공된 비헤이비어를 처음부터 다시 사용할 수도 있습니다.

## 기본 플레이어 만들기 {#section_30E4812C4DDA4B519C9C837930B6AE45}

`primetimevisualapi.min.js` 는 UI 프레임워크 라이브러리이며, 모든 기능이 전역 개체 ptp를 통해 노출됩니다. 다음 예제에서는 `videoPlayer` 메서드는 기본 플레이어를 만듭니다.

```js
<script src="scripts/primetimevisualapi.min.js"></script> 
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
    })(); 
</script>
```

## 플레이어 구성 {#section_9FC936B983CD40439E6D7675197B226C}

다음 방법 중 하나로 플레이어를 구성할 수 있습니다.

* JSON 개체 사용
* API 사용

JSON 개체를 생성하기 위해 브라우저 TVSDK는 UI Configurator 도구를 제공합니다. 도구에서 다양한 설정을 선택하고 **[!UICONTROL Test Configuration]** 을 클릭하여 설정을 확인하고 **[!UICONTROL Download Configuration]** 설정을 다운로드하려면 다음을 수행하십시오. 다운로드한 파일의 콘텐츠는 JSON 개체로 사용되어 로 전달됩니다. `ptp.videoPlayer` API.

**UI Configurator 도구를 실행하는 방법**:

1. 호스트 `frameworks` 로컬 웹 서버의 Browser TVSDK에서 사용할 수 있는 폴더입니다.
1. 도구를 열려면 브라우저를 열고 로 이동합니다. `< path-to-hosted-frameworks-folder>/ui-framework/ui-configurator/`.

**플레이어의 동작 구성**

다음 방법 중 하나로 플레이어 동작을 구성할 수 있습니다.

>[!TIP]
>
>일부 설정의 경우 두 옵션을 모두 사용할 수 있습니다.

* **videoBehavior API 사용** `ptp.videoPlayer` 반환: `ptp.videoBehavior`기본 비디오 플레이어를 구성할 수 있습니다. 일부 재생 관련 설정을 구성해야 하는 경우 이 옵션을 사용할 수 있습니다.

  ```js
  player.setAbrControlParameters ({object})
  ```

* **videoPlayer 함수에 구성 객체 전달** 이 개체를 사용하는 경우 위에서 설명한 재생 설정 외에 UI의 비헤이비어를 구성할 수 있습니다. 호출자는 변경해야 하는 매개 변수를 지정해야 하며 플레이어는 지정되지 않은 매개 변수에 대해 기본값을 계속 사용합니다.

  ```js
  var player = ptp.videoPlayer('#video1', { 
          player: { 
              abrControlParameters : {object} 
      }, 
      controlBar : {object} 
  });
  ```

  위의 예에서는 구성 객체를 사용하여 ABR 제어 매개변수를 구성했습니다. 컨트롤 막대 동작을 구성하기 위한 개체도 전달되었습니다.

  구성 객체의 구조에 대해서는 아래의 구성 객체 구조 보기 섹션을 참조하십시오.

* **AdobePSDK.MediaPlayer 액세스** 다음을 사용할 수 있습니다. `videoPlayer.getMediaPlayer` 브라우저 TVSDK의 MediaPlayer에 액세스해야 하는 특정 고급 사용 사례에서.

* **플레이어 스킨 구성** 플레이어 스키닝에 대한 자세한 내용은 다음을 참조하십시오. [선수 껍질 벗기기](../../browser-tvsdk-2.4/c-psdk-browser-2.4-userinterface/c-psdk-browser-tvsdk-2.4-skin-the-player.md).

## 기본 비헤이비어 수정 {#section_D5D692638FFF4BEF81F7BE70E438CCE9}

UI 프레임워크 용어에서 비헤이비어는 특정 구성 요소의 시각적 부분과 상호 작용 부분을 정의하는 구성입니다. 아래에 설명된 개체 구조를 사용하여 비헤이비어에서 변경하려는 사항을 수정할 수 있습니다.

예를 들어 볼륨 슬라이더가 표시되면 이를 숨기지 않으려면 다음 샘플을 사용합니다.

```js
var customVolumeSliderBehavior = function (element, configuration, player) { 
    function neverHide() { 
        // do nothing 
 } 
 
    var api = ptp.volumeSliderBehavior(element, configuration, player) 
        .compose({ 
            hide: neverHide 
 }); 
    return api; 
}; 
var player = ptp.videoPlayer('.videoHolder', { 
    controlBar : { 
        volume: { 
            slider: { 
                behavior: customVolumeSliderBehavior 
 } 
        } 
    } 
}
```

>[!NOTE]
>
>원하는 사용자 지정에 따라 비헤이비어의 특정 기능을 재정의하거나 자신만의 비헤이비어를 작성할 수 있습니다. 재정의할 수 있는 기능에 대한 자세한 내용은 [UI 프레임워크](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) API 설명서입니다.

## 참조 {#section_0A76A3F44D8A49B09FE4C83F3FACCB76}

다음은 몇 가지 추가 참조 정보입니다.

* **구성 객체 구조 보기** 이는 비헤이비어의 기본 요소와 함께 모든 기본 비헤이비어를 계층적 방식으로 언급하는 완전한 오브젝트 구조입니다. 샘플 구성에서는 UI 팩토리를 사용하여 요소를 만들었습니다. 동일한 방법이나 원하는 방법으로 요소를 구성할 수 있습니다.

  변경할 부품만 지정해야 하며 나머지 기능은 기본값에서 선택됩니다. 시작하려면 사용 사례에 따라 `SingleViewConfigurationObject` 또는 `MultiViewConfigurationObject` 구조입니다.

  ```js
  var DEFAULT_CONTROL_BAR_CONFIG = { 
      behavior: ptp.controlBarBehavior, 
      element: ptp.factories.simpleDivFactory(null, ptp.elementGetter(selector), 'ptp-control-bar'), 
      audioTrack: { 
          behavior: ptp.audioTrackButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('audioTrackBtn', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-audio-track ptp-control-bar-btn') 
      }, 
      closedCaption: { 
          behavior: ptp.closedCaptionButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('cc', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ' + 
              'ptp-btn-closed-caption ptp-control-bar-btn hidden', 
              'CC') 
      }, 
      displayTime: { 
          behavior: ptp.timeRemainingBehavior, 
          element: ptp.factories.simpleDivFactory('displayTime', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-txt-control ptp-txt-display-time') 
      }, 
      fastForward: { 
          behavior: ptp.fastForwardButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('fastForward', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-fastforward ptp-control-bar-btn', 
              'Fast Forward') 
      }, 
      fastRewind: { 
          behavior: ptp.fastRewindButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('fastRewind', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-fastrewind ptp-control-bar-btn', 
              'Fast Rewind') 
      }, 
      fullScreen: { 
          behavior: ptp.fullScreenButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('fullScreen', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-fullscreen ptp-control-bar-btn', 
              'Full Screen') 
      }, 
      moreOptions: { 
          behavior: ptp.moreOptionsButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('moreOptions', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-more-options ptp-control-bar-btn', 
              'More Options') 
      }, 
      multiView: { 
          behavior: ptp.multiViewButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('multiView', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-multiview ptp-control-bar-btn', 
              'Multi View') 
      }, 
      socialButton: { 
          behavior: ptp.shareVideoButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('shareVideo', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-share-video ptp-control-bar-btn', 
              'Share Video') 
      }, 
      volume: { 
          behavior: ptp.volumeBehavior, 
          element: ptp.factories.simpleDivFactory('volume', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-volume-control ptp-control-bar-btn'), 
          mute: { 
              behavior: ptp.muteButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('mute', ptp.elementGetter('.ptp-volume-control'), 
                  'ptp-control ptp-button-background ptp-btn-volume', 'Mute') 
          }, 
          slider: { 
              behavior: ptp.volumeSliderBehavior, 
              element: ptp.factories.simpleSliderFactory('volumeSlider', ptp.elementGetter('.ptp-volume-control'), 
                  'ptp-control ptp-volume-slider ptp-volume-hidden', 'Volume') 
          } 
      }, 
      pip: { 
          behavior: ptp.pipButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('pip', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-pip ptp-control-bar-btn', 'PIP') 
      }, 
      playPause: { 
          behavior: ptp.playPauseButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('play', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-playpause ptp-control-bar-btn', 
              'Play') 
      }, 
      rewind: { 
          behavior: ptp.rewindButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('rewind', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-rewind ptp-control-bar-btn', 
              'Rewind') 
      }, 
      scrubBar: { 
          element: ptp.factories.simpleDivFactory('scrubBar', ptp.elementGetter('.ptp-control-bar'), 'ptp-scrub-bar'), 
          behavior: ptp.scrubBarBehavior, 
   }, 
    bufferProgressBar: { 
              element: ptp.factories.simpleDivFactory('bufferProgressBar', ptp.elementGetter('.ptp-scrub-bar'), 
                  'ptp-buffer-progress-bar'), 
              behavior: ptp.bufferProgressBarBehavior 
    }, 
      seekToBar: { 
              element: ptp.factories.simpleDivFactory('seekToBar', ptp.elementGetter('.ptp-scrub-bar'), 'ptp-seek-to-bar'), 
              behavior: ptp.seekToBarBehavior 
    }, 
      playbackProgressBar: { 
              element: ptp.factories.simpleDivFactory('playbackProgressBar', ptp.elementGetter('.ptp-scrub-bar'), 
                  'ptp-playback-progress-bar'), 
              behavior: ptp.playProgressBarBehavior 
    }, 
      playHead: { 
              element: ptp.factories.simpleDivFactory('playHead', ptp.elementGetter('.ptp-scrub-bar'), 'ptp-progress-bar-play-head'), 
              behavior: ptp.playHeadBehavior 
    } 
      }, 
      slowRewind: { 
          behavior: ptp.slowRewindButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('slowRewind', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-slowrewind ptp-control-bar-btn', 
              'Slow Rewind'), 
          enabled: true 
   }, 
      slowForward: { 
          behavior: ptp.slowForwardButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('slowForward', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-slowforward ptp-control-bar-btn', 
              'Slow Forward') 
      }, 
      spacer: { 
          element: ptp.factories.simpleDivFactory('spacer', ptp.elementGetter('.ptp-control-bar'), 'ptp-fill-spacer') 
      }, 
      trickPlayRateDisplay: { 
          behavior: ptp.trickPlayRateDisplayBehavior, 
          element: ptp.factories.simpleDivFactory('trickPlayDisplay', 
              ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-control-bar-trick-play-rate hidden') 
      } 
  }; 
  var DEFAULT_LOCALIZATION_CONFIG = { 
      locale: 'en-US', 
      behavior: mapLocalizer, 
      localizationMap: { 
          'en-US': { 
              OK: 'Okay', 
              CANCEL: 'Cancel', 
              DEFAULT: 'Default', 
              NONE: 'None', 
              FONT_MONO_W_SERIF: 'Monospaced With Serifs', 
              FONT_PROP_W_SERIF: 'Proportional with Serifs', 
              FONT_MONO_WO_SERIF: 'Monospaced without Serifs', 
              FONT_CASUAL: 'Casual', 
              FONT_CURSIVE: 'Cursive', 
              FONT_SMALL_CAPS: 'Small Capitals', 
              FONT_EDGE_DEFAULT: 'Default', 
              FONT_EDGE_NONE: 'None', 
              FONT_EDGE_RAISED: 'Raised', 
              FONT_EDGE_DEPRESSED: 'Depressed', 
              FONT_EDGE_UNIFORM: 'Uniform', 
              FONT_EDGE_DROP_SHADOW_LEFT: 'Drop Shadow Left', 
              FONT_EDGE_DROP_SHADOW_RIGHT: 'Drop Shadow Right', 
              SIZE_SMALL: 'Small', 
              SIZE_MEDIUM: 'Medium', 
              SIZE_LARGE: 'Large', 
              COLOR_BLACK: 'Black', 
              COLOR_GREY: 'Grey', 
              COLOR_WHITE: 'White', 
              COLOR_BRIGHT_WHITE: 'Bright White', 
              COLOR_DARK_RED: 'Dark Red', 
              COLOR_RED: 'Red', 
              COLOR_BRIGHT_RED: 'Bright Red', 
              COLOR_DARK_GREEN: 'Dark Green', 
              COLOR_GREEN: 'Green', 
              COLOR_BRIGHT_GREEN: 'Bright Green', 
              COLOR_DARK_BLUE: 'Dark Blue', 
              COLOR_BLUE: 'Blue', 
              COLOR_BRIGHT_BLUE: 'Bright Blue', 
              COLOR_DARK_YELLOW: 'Dark Yellow', 
              COLOR_YELLOW: 'Yellow', 
              COLOR_BRIGHT_YELLOW: 'Bright Yellow', 
              COLOR_DARK_MAGENTA: 'Dark Magenta', 
              COLOR_MAGENTA: 'Magenta', 
              COLOR_BRIGHT_MAGENTA: 'Bright Magenta', 
              COLOR_DARK_CYAN: 'Dark Cyan', 
              COLOR_CYAN: 'Cyan', 
              COLOR_BRIGHT_CYAN: 'Bright Cyan', 
              REPLAY: 'Replay', 
              PLAY: 'Play', 
              PAUSE: 'Pause', 
              STOP: 'Stop' 
    } 
      } 
  }; 
  var DEFAULT_AUDIO_TRACK_SELECTION_CONFIG = { 
      behavior: ptp.audioTrackSelectionPanelBehavior, 
      element: ptp.factories.simpleDivFactory('audioTrackSelectionPanel', ptp.elementGetter(selector), 
          'ptp-audio-track-selection-panel hidden'), 
      audioTrackSelectionPanelHeader: { 
          behavior: ptp.audioTrackSelectionPanelHeader, 
          element: ptp.factories.simpleDivFactory('header', ptp.elementGetter('.ptp-audio-track-selection-panel'), 
              'ptp-panel-header ptp-audio-track-selection-header'), 
          audioTrackSelectionPanelCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closeButton', ptp.elementGetter('.ptp-audio-track-selection-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          audioTrackSelectionPanelTitle: { 
              element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-audio-track-selection-header'), 
                  'ptp-panel-title', 'Audio Track') 
          } 
      }, 
      audioTrackSelectionPanelSeparator: { 
          element: ptp.factories.simpleHRFactory('audioTrackSelectionPanelSeparator', 
              ptp.elementGetter('.ptp-audio-track-selection-panel'), 'ptp-hr-separator') 
      }, 
      audioTrackSelectionMenu: { 
          behavior: ptp.audioTrackSelectionMenu, 
          element: ptp.factories.simpleDivFactory('audioTrackSelectionMenu', ptp.elementGetter('.ptp-audio-track-selection-panel'), 
              'ptp-audio-track-selection-menu', 'Menu TBD') 
      } 
  }; 
  
  var DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG = { 
      behavior: ptp.closedCaptionLanguagePanelBehavior, 
      element: ptp.factories.simpleDivFactory('closedCaptionLanguagePanel', ptp.elementGetter(selector), 
          'ptp-closed-caption-panel hidden ptp-closed-caption-language-panel'), 
      closedCaptionLanguagePanelHeader: { 
          behavior: ptp.closedCaptionLanguagePanelHeader, 
          element: ptp.factories.simpleDivFactory('header', ptp.elementGetter('.ptp-closed-caption-language-panel'), 
              'ptp-panel-header ptp-closed-caption-language-header'), 
          closedCaptionLanguageCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closeButton', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          closedCaptionLanguageTitle: { 
              element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                  'ptp-panel-title', 'Closed Captions') 
          }, 
          closedCaptionLanguageOptionsButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                  'ptp-closed-caption-options-btn', 'Options') 
          } 
      }, 
      closedCaptionLanguageSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionLanguageSeparator', ptp.elementGetter('.ptp-closed-caption-panel'), 
              'ptp-hr-separator') 
      }, 
      closedCaptionOptions: { 
          behavior: ptp.closedCaptionLanguageMenu, 
          element: ptp.factories.simpleDivFactory('captionLanguageMenu', ptp.elementGetter('.ptp-closed-caption-panel'), 
              'ptp-scroll-bar ptp-closed-caption-language-menu') 
      } 
  }; 
  
  var DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG = { 
      behavior: ptp.closedCaptionOptionsPanelBehavior, 
      element: ptp.factories.simpleDivFactory('closedCaptionOptionsPanel', ptp.elementGetter(selector), 
          'ptp-closed-caption-panel hidden ptp-closed-caption-options-panel'), 
      closedCaptionOptionsHeader: { 
          behavior: ptp.closedCaptionOptionsPanelHeader, 
          element: ptp.factories.simpleDivFactory('closedCaptionOptionsHeader', ptp.elementGetter('.ptp-closed-caption-options-panel'), 
              'ptp-panel-header ptp-closed-caption-options-header'), 
          closedCaptionOptionsCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsCloseButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', '<') 
          }, 
          closedCaptionOptionsTitle: { 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsTitle', 
                  ptp.elementGetter('.ptp-closed-caption-options-header'), 'ptp-panel-title', 'Closed Captions') 
          }, 
          closedCaptionLanguageDoneButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionLanguageDoneButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-header'), 'ptp-closed-caption-done-btn', 'Done') 
          } 
      }, 
      closedCaptionOptionsHeaderSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionOptionsHeaderSeparator', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
      }, 
      closedCaptionOptionsMenu: { 
          behavior: ptp.closedCaptionOptionsMenu, 
          element: ptp.factories.simpleDivFactory('closedCaptionOptionsMenu', ptp.elementGetter('.ptp-closed-caption-options-panel'), 
              'ptp-closed-caption-options-menu'), 
          closedCaptionOptionsMainMenu: { 
              behavior: ptp.closedCaptionOptionsMainMenu, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsMainMenu', 
                  ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                  'ptp-scroll-bar ptp-closed-caption-options-main-menu'), 
              closedCaptionOptionsFontStyle: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontStyle', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Style') 
              }, 
              closedCaptionOptionsFontSize: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontSize', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Size') 
              }, 
              closedCaptionOptionsFontColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Color') 
              }, 
              closedCaptionOptionsFontOpacity: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontOpacity', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Opacity') 
              }, 
              closedCaptionOptionsBackgroundColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Background Color') 
              }, 
              closedCaptionOptionsBackgroundOpacity: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundOpacity', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Background Opacity') 
              }, 
              closedCaptionOptionsFillColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Fill Color') 
              }, 
              closedCaptionOptionsFillOpacity: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillOpacity', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Fill Opacity') 
              }, 
              closedCaptionOptionsFontEdge: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdge', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Stroke Weight') 
              }, 
              closedCaptionOptionsFontEdgeColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Stroke Color') 
              } 
          }, 
          closedCaptionOptionsMenuSeparator: { 
              element: ptp.factories.simpleHRFactory('closedCaptionOptionsMenuSeparator', 
                  ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                  'ptp-closed-caption-options-menu-separator') 
          }, 
          closedCaptionOptionsSubMenu: { 
              behavior: ptp.closedCaptionOptionsSubMenu, 
              closedCaptionOptionsFontStyleSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontStyleSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontEdgeSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontEdgeColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontSizeSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontSizeSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontOpacitySubMenu: { 
                  behavior: ptp.sliderMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontOpacitySubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
              }, 
              closedCaptionOptionsBackgroundColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsBackgroundOpacitySubMenu: { 
                  behavior: ptp.sliderMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundOpacitySubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
              }, 
              closedCaptionOptionsFillColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFillOpacitySubMenu: { 
                  behavior: ptp.sliderMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillOpacitySubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
              } 
          } 
      }, 
      closedCaptionOptionsPreviewSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionOptionsPreviewSeparator', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
      }, 
      closedCaptionPreviewPanel: { 
          behavior: ptp.closedCaptionPreviewPanel, 
          text: 'Sample Captions', 
          element: ptp.factories.simpleDivFactory('closedCaptionPreviewPanel', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 
              'ptp-closed-caption-preview-panel', 'Sample Captions') 
      }, 
      closedCaptionOptionsFooterSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionOptionsFooterSeparator', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
      }, 
      closedCaptionOptionsFooter: { 
          behavior: ptp.closedCaptionOptionsFooter, 
          element: ptp.factories.simpleDivFactory('closedCaptionOptionsFooter', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-closed-caption-options-footer'), 
          closedCaptionOptionsResetButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsResetButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-footer'), 
                  'ptp-closed-caption-options-reset-button', 'Reset to Default') 
          }, 
          closedCaptionOptionsApplyButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsApplyButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-footer'), 
                  'ptp-closed-caption-options-apply-button', 'Apply') 
          } 
      } 
  }; 
  
  var DEFAULT_SHARE_VIDEO_PANEL_CONFIG = { 
      behavior: ptp.shareVideoPanelBehavior, 
      element: ptp.factories.simpleDivFactory('shareVideoPanel', ptp.elementGetter(selector), 'ptp-share-video-panel hidden'), 
      shareVideoPanelHeader: { 
          behavior: ptp.shareVideoPanelHeader, 
          element: ptp.factories.simpleDivFactory('shareVideoPanelHeader', ptp.elementGetter('.ptp-share-video-panel'), 
              'ptp-panel-header ptp-share-video-panel-header'), 
          shareVideoPanelCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelCloseButton', ptp.elementGetter('.ptp-share-video-panel-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          shareVideoPanelTitle: { 
              element: ptp.factories.simpleDivFactory('shareVideoPanelTitle', ptp.elementGetter('.ptp-share-video-panel-header'), 
                  'ptp-panel-title', 'Social Share') 
          } 
      }, 
      shareVideoPanelHeaderSeparator: { 
          element: ptp.factories.simpleHRFactory('shareVideoPanelHeaderSeparator', ptp.elementGetter('.ptp-share-video-panel'), 
              'ptp-hr-separator') 
      }, 
      shareVideoPanelMenu: { 
          element: ptp.factories.simpleDivFactory('shareVideoPanelMenu', ptp.elementGetter('.ptp-share-video-panel'), 
              'share-video-panel-menu'), 
          behavior: ptp.shareVideoPanelMenu, 
          shareVideoPanelFacebookBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelFacebookBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-facebook') 
          }, 
          shareVideoPanelTwitterBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelTwitterBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-twitter') 
          }, 
          shareVideoPanelGoogleBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelGoogleBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-google-plus') 
          }, 
          shareVideoPanelLinkedinBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelLinkedinBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-linkedin') 
          } 
      } 
  }; 
  
  var DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG = { 
      behavior: ptp.moreOptionsControlPanel, 
      element: ptp.factories.simpleDivFactory('moreOptionsControlPanel', ptp.elementGetter(selector), 
          'ptp-more-options-control-panel hidden'), 
      moreOptionsControlPanelHeader: { 
          behavior: ptp.moreOptionsControlPanelHeader, 
          element: ptp.factories.simpleDivFactory('moreOptionsControlPanelHeader', 
              ptp.elementGetter('.ptp-more-options-control-panel'), 
              'ptp-panel-header ptp-more-options-control-panel-header'), 
          moreOptionsControlPanelCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('moreOptionsControlPanelCloseButton', 
                  ptp.elementGetter('.ptp-more-options-control-panel-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          moreOptionsControlPanelTitle: { 
              element: ptp.factories.simpleDivFactory('moreOptionsPanelTitle', 
                  ptp.elementGetter('.ptp-more-options-control-panel-header'), 
                  'ptp-panel-title', 'Options') 
          } 
      }, 
      moreOptionsPanelHeaderSeparator: { 
          element: ptp.factories.simpleHRFactory('moreOptionsPanelHeaderSeparator', 
              ptp.elementGetter('.ptp-more-options-control-panel'), 
              'ptp-hr-separator') 
      }, 
      moreOptionsPanelMenu: { 
          element: ptp.factories.simpleDivFactory('moreOptionsPanelMenu', 
              ptp.elementGetter('.ptp-more-options-control-panel'), 
              'ptp-more-options-control-panel-menu'), 
          behavior: ptp.moreOptionsControlPanelMenu, 
          audioTrackButton: { 
              behavior: ptp.audioTrackButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('audioTrackBtn', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-audio-track ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 
                  'Audio Track') 
          }, 
          multiViewButton: { 
              behavior: ptp.multiViewButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('multiView', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-multiview ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 
                  'Multi View') 
          }, 
          pipButton: { 
              behavior: ptp.pipButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('pip', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-pip ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 'PIP') 
          }, 
          socialButton: { 
              behavior: ptp.shareVideoButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('shareVideo', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-share-video ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 
                  'Share Video') 
          } 
      } 
  }; 
  
  SingleViewConfigurationObject = { 
      element: ptp.elementGetter(selector), 
      classNames: 'ptp-root-element', 
      behavior: ptp.singleViewBehavior, 
      logLevel: 0, 
      logOutput: null, 
      player: { 
          element: ptp.factories.simpleDivFactory('videoPlayer', ptp.elementGetter(selector), 
              'ptp-main-video-div-style ptp-background-style'), 
          behavior: ptp.videoBehavior, 
          autoPlay: true, 
          bufferingOverlay: { 
              behavior: ptp.bufferingOverlayBehavior, 
              element: ptp.createDiv('bufferingOverlay', ptp.elementGetter('.ptp-main-video-div-style'), 'ptp-buffering-overlay') 
          }, 
          errorMessagePanel: { 
              behavior: ptp.errorMessagePanelBehavior, 
              element: ptp.createDiv('errorMessagePanel', ptp.elementGetter('.ptp-main-video-div-style'), 'ptp-error-message-panel hidden') 
          }, 
          controlsDisabledInAd: //same as ptp.videoBehavior.setControlsDisabledInAd  
   mediaPlayerItemConfig: //same as ptp.videoBehavior.setMediaPlayerItemConfig  
     abrControlParameters: //same as ptp.videoBehavior.setAbrControlParameters  
    bufferControlParameters: //same as ptp.videoBehavior.setBufferControlParameters  
    ccVisibility: //same as ptp.videoBehavior.setCCVisibility  
     ccStyle: //same as ptp.videoBehavior.setCCStyle  
    mediaResource: //same as ptp.videoBehavior.setMediaResource  
    volume: //same as ptp.videoBehavior.setVolume 
    }, 
  
      pip: { 
          element: ptp.factories.simpleDivFactory('pip', ptp.elementGetter(selector), 'ptp-pip-video-div'), 
              behavior: ptp.videoBehavior, 
              bufferingOverlay: { 
              behavior: ptp.bufferingOverlayBehavior, 
                  element: ptp.createDiv('bufferingOverlay', ptp.elementGetter('.ptp-pip-video-div'), 'ptp-buffering-overlay') 
          }, 
          errorMessagePanel: { 
              behavior: ptp.errorMessagePanelBehavior, 
                  element: ptp.createDiv('errorMessagePanel', ptp.elementGetter('.ptp-pip-video-div'), 'ptp-error-message-panel hidden') 
          }, 
          autoPlay: false 
    }, 
      localization: DEFAULT_LOCALIZATION_CONFIG, 
      controlBar: DEFAULT_CONTROL_BAR_CONFIG, 
      audioTrackSelectionPanel: DEFAULT_AUDIO_TRACK_SELECTION_CONFIG, 
      closedCaptionLanguagePanel: DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG, 
      closedCaptionOptionsPanel: DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG, 
      moreOptionsControlPanel: DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG, 
      shareVideoPanel: DEFAULT_SHARE_VIDEO_PANEL_CONFIG 
  }; 
  
  MultiViewConfigurationObject = { 
      element: ptp.elementGetter(selector), 
      classNames: 'ptp-root-element', 
      behavior: ptp.multiViewBehavior, 
      logLevel: 0, 
      logOutput: null, 
      multiVideoHolder: { 
          element: ptp.factories.simpleDivFactory('multiViewPlayer', ptp.elementGetter(selector), 'ptp-multi-view-container') 
      }, 
      views: [ 
          { 
              player: {} // see in SingleViewConfigurationObject above 
    } 
      ], 
      localization: DEFAULT_LOCALIZATION_CONFIG, 
      controlBar: DEFAULT_CONTROL_BAR_CONFIG, 
      audioTrackSelectionPanel: DEFAULT_AUDIO_TRACK_SELECTION_CONFIG, 
      closedCaptionLanguagePanel: DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG, 
      closedCaptionOptionsPanel: DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG, 
      moreOptionsControlPanel: DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG, 
      shareVideoPanel: DEFAULT_SHARE_VIDEO_PANEL_CONFIG 
  };
  ```

* **도우미 구문** 이 구문은 다음과 같이 구성됩니다.

   * **공장** 시각적 요소를 만들려면 다음을 사용할 수 있습니다 `ptp.factories.simpleButtonFactory`, `ptp.factories.simpleDivFactory`, `ptp.factories.simpleHRFactory`, 및 `ptp.factories.simpleSliderFactory`. 자세한 내용은 [UI 프레임워크](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) API 설명서입니다.

   * **Mixins** Mixin은 일반적인 구문을 사용하도록 비헤이비어에서 구성할 수 있는 구성 가능한 모듈입니다. 예를 들어, 많은 구성 요소는 예를 들어 광고가 재생될 때 동작에 영향을 줄 수 있는 변경 사항을 인식하려고 합니다. 이러한 모든 요소는 `adBreak` 클래스.

     다음은 기본 제공 mixin 구현 방법에 대한 예입니다 `adBreakStyling`:

     ```js
     adBreakStyling = function (element, player) { 
         ... 
         ... 
         return composable().compose({ 
             init: init, 
             manageAdBreakStyle: manageAdBreakStyle 
      }); 
     }
     ```

     비헤이비어가 이 mixin을 사용하는 방법은 다음과 같습니다.

     ```js
     customBehavior = function (element, configuration, player) { 
         var api = 
             component(element, configuration, player, clickHandler).compose( 
                 adBreakStyling(element, player).compose({ 
                     init: init, 
                 })); 
         return api; 
     }
     ```

     지금 `customBehavior` 에 의해 노출된 모든 메서드를 사용할 수 있습니다. `adBreakStyling`, 이 예에서 는 `manageAdBreakStyle`. 한 가지 추가 사용 사례는 mixin이 이벤트 리스너를 추가할 수 있고 핸들러에서 mixin이 어떤 식으로든 요소를 수정할 수 있는 경우입니다. 그러면 이 mixin을 사용하는 구성 요소에 이 기능이 자동으로 제공됩니다.

   * **유틸리티** 다음과 같은 일부 유틸리티 `ptp.elementGetter`: 구성 섹션 및 `ptp.deepmerge`을 사용하면 비헤이비어를 작성하거나 확장하는 데 도움이 될 수 있습니다. 자세한 내용은 [UI 프레임워크](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) API 설명서입니다.

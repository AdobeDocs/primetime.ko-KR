---
description: PTMediaPlayer 인터페이스는 미디어 플레이어 개체의 기능 및 동작을 캡슐화합니다.
title: PTMediaPlayer 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# PTMediaPlayer 설정 {#set-up-the-ptmediaplayer}

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 만드는 도구를 제공합니다.

플랫폼의 도구를 사용하여 플레이어를 만들고 TVSDK의 미디어 플레이어 보기에 연결하십시오. 이 보기에는 비디오를 재생하고 관리하는 메서드가 있습니다. 예를 들어 TVSDK는 재생 및 일시 중지 메서드를 제공합니다. 플랫폼에서 사용자 인터페이스 단추를 만들고 해당 TVSDK 메서드를 호출하도록 단추를 설정할 수 있습니다.

PTMediaPlayer 인터페이스는 미디어 플레이어 개체의 기능 및 동작을 캡슐화합니다.

을(를) 설정하려면 `PTMediaPlayer`:

1. 사용자 인터페이스에서 미디어의 URL을 가져옵니다(예: 텍스트 필드).

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. 만들기 `PTMetadata`.

   메서드를 사용한다고 가정해 보십시오. `createMetada` 메타데이터 준비(참조) [광고](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. 만들기 `PTMediaPlayerItem` 을(를) 사용하여 `PTMetadata` 인스턴스.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. TVSDK가 전달하는 알림에 관찰자를 추가합니다.

   ```
   [self addObservers]
   ```

1. 만들기 `PTMediaPlayer` 새 항목 사용 `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 플레이어에 대한 속성을 설정합니다.

   사용 가능한 항목 몇 가지는 다음과 같습니다 `PTMediaPlayer` 속성:

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. 플레이어의 보기 속성을 설정합니다.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. 현재 보기의 하위 보기에서 플레이어 보기를 추가합니다.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. 호출 `play` 미디어 재생을 시작합니다.

   ```
   [player play];
   ```

---
description: PTMediaPlayer 인터페이스는 미디어 플레이어 객체의 기능과 비헤이비어를 캡슐화합니다.
title: PTMediaPlayer 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# PTMediaPlayer {#set-up-the-ptmediaplayer} 설정

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하기 위한 툴을 제공합니다.

플랫폼의 툴을 사용하여 플레이어를 만들고 TVSDK의 미디어 플레이어 보기에 연결하여 비디오를 재생하고 관리하는 방법을 살펴봅니다. 예를 들어 TVSDK는 재생 및 일시 정지 메서드를 제공합니다. 플랫폼에서 사용자 인터페이스 단추를 만들고 해당 TVSDK 메서드를 호출하도록 단추를 설정할 수 있습니다.

PTMediaPlayer 인터페이스는 미디어 플레이어 객체의 기능과 비헤이비어를 캡슐화합니다.

`PTMediaPlayer`을(를) 설정하려면:

1. 사용자 인터페이스에서 미디어 URL을 가져옵니다(예: 텍스트 필드).

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. `PTMetadata`을(를) 만듭니다.

   메서드 `createMetada`이(가) 메타데이터를 준비한다고 가정합니다([광고](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md) 참조).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. `PTMetadata` 인스턴스를 사용하여 `PTMediaPlayerItem`을(를) 만듭니다.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. TVSDK가 전달하는 알림에 옵저버를 추가합니다.

   ```
   [self addObservers]
   ```

1. 새 `PTMediaPlayerItem`을(를) 사용하여 `PTMediaPlayer`을(를) 만듭니다.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 플레이어에서 속성을 설정합니다.

   다음은 사용 가능한 `PTMediaPlayer` 속성 중 일부입니다.

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

1. 현재 보기의 하위 보기에서 플레이어의 보기를 추가합니다.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. 미디어 재생을 시작하려면 `play`을(를) 호출합니다.

   ```
   [player play];
   ```


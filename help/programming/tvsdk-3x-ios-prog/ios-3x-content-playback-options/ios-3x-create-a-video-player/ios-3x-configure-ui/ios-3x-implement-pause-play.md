---
description: 미디어를 일시 중지하고 재생하기 위해 TVSDK 메서드를 호출하는 단추를 설정할 수 있습니다.
seo-description: 미디어를 일시 중지하고 재생하기 위해 TVSDK 메서드를 호출하는 단추를 설정할 수 있습니다.
seo-title: 재생/일시 정지 단추 구현
title: 재생/일시 정지 단추 구현
uuid: b0ce4103-819e-4a1c-8238-1d7728ec8770
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# 재생/일시 정지 단추 {#implement-a-play-pause-button} 구현

미디어를 일시 중지하고 재생하기 위해 TVSDK 메서드를 호출하는 단추를 설정할 수 있습니다.

다음 샘플 코드를 사용하여 재생 또는 일시 정지 단추를 구현합니다.

<!--<a id="example_BC2632D673FE451190A30A23145090D0"></a>-->

```
_playPauseButton =  
[[UIButton alloc] initWithFrame:CGRectMake(BUTTON_POS_X, BUTTON_POS_Y, BUTTON_SIZE_W, BUTTON_SIZE_H)]; 
[_playPauseButton setImage:[UIImage imageNamed:@"play.png"] forState:UIControlStateNormal];  
[_playPauseButton setImage:[UIImage imageNamed:@"pause.png"] forState:UIControlStateSelected]; 
[_playPauseButton addTarget:self action:@selector(playTouch:) forControlEvents:UIControlEventTouchUpInside]; 
[self addSubview:_playPauseButton]; 
 
... 
 
- (void)playTouch:(id)sender { 
    if (self.player.status == PTMediaPlayerStatusPlaying) { 
        _playPauseButton.selected = YES;  
        [self.player pause]; 
    } 
    else { 
        _playPauseButton.selected = NO; [self.player play]; 
    } 
} 
```

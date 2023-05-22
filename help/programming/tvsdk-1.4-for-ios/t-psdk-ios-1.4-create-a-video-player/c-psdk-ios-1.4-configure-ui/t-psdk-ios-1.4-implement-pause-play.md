---
description: TVSDK 메서드를 호출하는 버튼을 설정하여 미디어를 일시 중지하고 재생할 수 있습니다.
title: 재생/일시 중지 버튼 구현
exl-id: 72b90a67-d5a3-4575-a67e-58a0f0d0acf1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# 재생/일시 중지 버튼 구현{#implement-a-play-pause-button}

TVSDK 메서드를 호출하는 버튼을 설정하여 미디어를 일시 중지하고 재생할 수 있습니다.

다음 샘플 코드를 사용하여 재생 또는 일시 중지 버튼을 구현합니다.

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

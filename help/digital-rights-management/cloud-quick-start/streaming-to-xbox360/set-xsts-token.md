---
title: 플레이어에서 XSTS 토큰 설정
description: 플레이어에서 XSTS 토큰 설정
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# 플레이어에서 XSTS 토큰 설정{#set-the-xsts-token-in-your-player}

Xbox360에서는 다음에 대한 응답으로 토큰을 비동기적으로 설정합니다. `MediaPlayer.RequestKeyAttribute` 이벤트.

XSTS 토큰을 설정합니다.

소프트웨어와 함께 번들로 제공되는 샘플 앱은 플레이어에서 XSTS 토큰을 설정하는 방법을 보여 줍니다. 다음은 샘플 플레이어의 관련 코드 조각입니다.

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```


---
description: 'null'
seo-description: 'null'
seo-title: 플레이어에서 XSTS 토큰 설정
title: 플레이어에서 XSTS 토큰 설정
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# 플레이어에서 XSTS 토큰 설정{#set-the-xsts-token-in-your-player}

Xbox360에서는 `MediaPlayer.RequestKeyAttribute` 이벤트에 대한 비동기식으로 토큰을 설정합니다.

XSTS 토큰을 설정합니다.

소프트웨어와 함께 번들로 제공되는 샘플 앱은 플레이어에서 XSTS 토큰을 설정하는 방법을 보여줍니다. 다음은 샘플 플레이어의 관련 코드 조각입니다.

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


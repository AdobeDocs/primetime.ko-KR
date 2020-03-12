---
description: DRMAuthenticateEvent 개체는 Primetime 개체가 재생 전에 인증을 위해 사용자 자격 증명이 필요한 보호된 콘텐츠를 재생하려고 할 때 전달됩니다(아직 인증이 수행되지 않음). DRMAuthenticateEvent 핸들러는 필요한 자격 증명(사용자 이름, 암호 및 유형)을 수집하고 유효성 검사를 위해 .setDRMAuthenticationCredentials() 메서드에 값을 전달합니다.
seo-description: DRMAuthenticateEvent 개체는 Primetime 개체가 재생 전에 인증을 위해 사용자 자격 증명이 필요한 보호된 콘텐츠를 재생하려고 할 때 전달됩니다(아직 인증이 수행되지 않음). DRMAuthenticateEvent 핸들러는 필요한 자격 증명(사용자 이름, 암호 및 유형)을 수집하고 유효성 검사를 위해 .setDRMAuthenticationCredentials() 메서드에 값을 전달합니다.
seo-title: DRMAuthenticateEvent 핸들러 만들기
title: DRMAuthenticateEvent 핸들러 만들기
uuid: 58330691-d0b5-46bd-9b1d-8dc597580d31
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# DRMAuthenticateEvent 핸들러 만들기{#create-a-drmauthenticateevent-handler}

DRMAuthenticateEvent 개체는 Primetime 개체가 재생 전에 인증을 위해 사용자 자격 증명이 필요한 보호된 콘텐츠를 재생하려고 할 때 전달됩니다(아직 인증이 수행되지 않음). DRMAuthenticateEvent 핸들러는 필요한 자격 증명(사용자 이름, 암호 및 유형)을 수집하고 유효성 검사를 위해 .setDRMAuthenticationCredentials() 메서드에 값을 전달합니다.

응용 프로그램은 사용자 자격 증명을 얻기 위한 몇 가지 메커니즘을 제공해야 합니다. 예를 들어, 응용 프로그램은 사용자에게 사용자 이름과 암호 값을 입력하는 간단한 사용자 인터페이스를 제공할 수 있습니다. 또한 반복되는 인증 실패 시도를 처리하고 제한하는 메커니즘을 제공해야 합니다.

이벤트를 발생시킨 Primetime 개체에 하드 코딩된 인증 자격 증명 집합을 전달하는 이벤트 핸들러를 만듭니다.

```
var connection:NetConnection = new NetConnection();  
connection.connect(null);  
var videoStream:Primetime = new Primetime(connection);  
 
videoStream.addEventListener( 
  DRMAuthenticateEvent.DRM_AUTHENTICATE,  
  drmAuthenticateEventHandler)  
  private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
    videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
} 
```

비디오를 재생하고 비디오 스트림에 성공적으로 연결되었는지 확인하는 코드는 여기에 포함되어 있지 않습니다.

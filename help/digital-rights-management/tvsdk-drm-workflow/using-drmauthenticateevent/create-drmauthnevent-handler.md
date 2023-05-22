---
description: Primetime 개체가 재생 전에 인증을 위해 사용자 자격 증명이 필요한 보호된 콘텐츠를 재생하려고 할 때(아직 인증이 수행되지 않음) DRMAuthenticationEvent 개체가 발송됩니다. DRMAuthenticationEvent 처리기는 필수 자격 증명(사용자 이름, 암호 및 유형)을 수집하고 유효성 검사를 위해 .setDRMAuthenticationCredentials() 메서드에 값을 전달하는 역할을 합니다.
title: DRMAuthenticationEvent 처리기 만들기
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# DRMAuthenticationEvent 처리기 만들기{#create-a-drmauthenticateevent-handler}

Primetime 개체가 재생 전에 인증을 위해 사용자 자격 증명이 필요한 보호된 콘텐츠를 재생하려고 할 때(아직 인증이 수행되지 않음) DRMAuthenticationEvent 개체가 발송됩니다. DRMAuthenticationEvent 처리기는 필수 자격 증명(사용자 이름, 암호 및 유형)을 수집하고 유효성 검사를 위해 .setDRMAuthenticationCredentials() 메서드에 값을 전달하는 역할을 합니다.

응용 프로그램은 사용자 자격 증명을 얻기 위한 몇 가지 메커니즘을 제공해야 합니다. 예를 들어, 애플리케이션은 사용자에게 사용자 이름과 암호 값을 입력할 수 있는 간단한 사용자 인터페이스를 제공할 수 있습니다. 또한 반복되는 인증 실패 시도를 처리하고 제한하는 메커니즘을 제공해야 합니다.

이벤트를 발생시킨 Primetime 개체에 하드 코딩된 인증 자격 증명 집합을 전달하는 이벤트 처리기를 만듭니다.

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

(비디오를 재생하고 비디오 스트림에 성공적으로 연결되었는지 확인하는 코드는 여기에 포함되지 않습니다.)

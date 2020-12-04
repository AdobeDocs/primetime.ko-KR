---
seo-title: DRMErrorEvent 클래스 개요 사용
title: DRMErrorEvent 클래스 개요 사용
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# DRMErrorEvent 클래스 사용 {#using-the-drmerrorevent-class}

Primetime은 보호된 콘텐츠를 재생하려고 하는 Primetime 개체가 `DRMErrorEvent` 개체에 [DRM 관련 오류](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)이(가) 나타날 때 이를 전달합니다. 사용자 자격 증명이 잘못된 경우 사용자가 유효한 자격 증명을 입력하거나 응용 프로그램이 추가 시도를 거부할 때까지 `DRMAuthenticateEvent` 개체가 반복적으로 전달합니다. 애플리케이션은 [DRM 관련 오류](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)을 감지하고 식별 및 처리하기 위해 다른 DRM 오류 이벤트를 수신해야 합니다.

유효한 사용자 자격 증명이 있더라도 컨텐츠 라이선스 약관은 사용자가 암호화된 내용을 볼 수 없도록 할 수 있습니다. 예를 들어 허가되지 않은 응용 프로그램에서 컨텐트를 보려고 시도하는 경우(예: 응용 프로그램 허용 목록) 사용자에게 액세스가 거부될 수 있습니다. 허가되지 않은 응용 프로그램은 나열된 응용 프로그램 서명 인증서로 서명되지 않은 응용 프로그램입니다. 이 경우 `DRMErrorEvent` 개체가 전달됩니다.

컨텐츠가 손상되거나 애플리케이션의 버전이 라이센스에서 지정한 버전과 일치하지 않는 경우에도 오류 이벤트를 실행할 수 있습니다. 응용 프로그램은 오류를 처리하는 적절한 메커니즘을 제공해야 합니다.

## DRMErrorEvent 핸들러 {#create-a-drmerrorevent-handler} 만들기

보호된 콘텐츠를 재생하는 동안 오류가 발생하면 Primetime에서 발송된 오류 이벤트를 처리하는 이벤트 핸들러를 만듭니다.

일반적으로 응용 프로그램에 오류가 발생하면 많은 수의 정리 작업을 수행합니다. 그런 다음 사용자에게 오류를 알리고 문제 해결을 위한 옵션을 제공합니다.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

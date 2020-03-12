---
seo-title: DRMErrorEvent 클래스 개요 사용
title: DRMErrorEvent 클래스 개요 사용
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# DRMErrorEvent 클래스 사용 {#using-the-drmerrorevent-class}

Primetime은 보호된 콘텐츠를 재생하려고 하는 Primetime 개체에 DRM `DRMErrorEvent` 관련 오류가 [](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)발생하면 개체를 전달합니다. 사용자 자격 증명이 잘못된 경우 사용자가 유효한 자격 증명을 입력하거나 응용 프로그램이 추가 시도를 거부할 때까지 개체가 반복적으로 전달됩니다. `DRMAuthenticateEvent` 애플리케이션은 DRM 관련 오류를 감지, 식별 및 처리하기 위해 다른 DRM 오류 이벤트를 [수신해야](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)합니다.

유효한 사용자 자격 증명을 사용하더라도 콘텐트 사용권 조항은 사용자가 암호화된 내용을 볼 수 없도록 할 수 있습니다. 예를 들어 허가되지 않은 응용 프로그램(예: 응용 프로그램 화이트리스트)에서 컨텐츠를 보려고 시도하면 사용자가 액세스가 거부될 수 있습니다. 권한 없는 응용 프로그램은 화이트리스트 등록 응용 프로그램 서명 인증서로 서명되지 않은 응용 프로그램입니다. 이 경우 `DRMErrorEvent` 개체가 전달됩니다.

컨텐츠가 손상되거나 애플리케이션의 버전이 라이센스에 지정된 버전과 일치하지 않는 경우에도 오류 이벤트를 실행할 수 있습니다. 응용 프로그램은 오류 처리를 위한 적절한 메커니즘을 제공해야 합니다.

## DRMErrorEvent 핸들러 만들기 {#create-a-drmerrorevent-handler}

보호된 콘텐츠를 재생하는 동안 오류가 발생하면 Primetime에서 전달된 오류 이벤트를 처리하는 이벤트 핸들러를 만듭니다.

일반적으로 응용 프로그램에 오류가 발생하면 정리 작업을 여러 번 수행합니다. 그런 다음 사용자에게 오류를 알리고 문제 해결을 위한 옵션을 제공합니다.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

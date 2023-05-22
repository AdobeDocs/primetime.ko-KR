---
title: DRMErrorEvent 클래스 개요 사용
description: DRMErrorEvent 클래스 개요 사용
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# DRMErrorEvent 클래스 개요 사용 {#using-the-drmerrorevent-class-overview}

Primetime에서 `DRMErrorEvent` Primetime 개체가 보호된 콘텐츠를 재생하려고 할 때 [DRM 관련 오류](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). 사용자 자격 증명이 유효하지 않은 경우 `DRMAuthenticateEvent` 사용자가 유효한 자격 증명을 입력하거나 애플리케이션에서 추가 시도를 거부할 때까지 개체가 반복적으로 디스패치됩니다. 애플리케이션은 를 감지하고 식별하고 처리하기 위해 다른 DRM 오류 이벤트를 수신합니다 [DRM 관련 오류](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

유효한 사용자 자격 증명이 있더라도 콘텐츠 라이선스의 약관은 여전히 사용자가 암호화된 콘텐츠를 볼 수 없게 할 수 있습니다. 예를 들어, 사용자는 승인되지 않은 애플리케이션(예: 애플리케이션 허용 목록)에서 콘텐츠를 보려고 시도하기 위한 액세스가 거부될 수 있습니다. 허가되지 않은 응용 프로그램은 허용 목록에 있는 응용 프로그램 서명 인증서로 서명되지 않은 응용 프로그램입니다. 이 경우 a `DRMErrorEvent` 개체가 발송되었습니다.

콘텐츠가 손상되었거나 응용 프로그램의 버전이 라이선스에서 지정한 버전과 일치하지 않는 경우에도 오류 이벤트가 발생할 수 있습니다. 응용 프로그램은 오류를 처리할 수 있는 적절한 메커니즘을 제공해야 합니다.

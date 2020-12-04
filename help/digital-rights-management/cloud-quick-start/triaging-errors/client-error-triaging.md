---
description: 경우에 따라 콘텐트를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 많은 경우 이로 인해 발생할 수 있습니다.
seo-description: 경우에 따라 콘텐트를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 많은 경우 이로 인해 발생할 수 있습니다.
seo-title: 트리징 오류 개요
title: 트리징 오류 개요
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# 트리밍 오류 {#triaging-errors}

경우에 따라 콘텐트를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 많은 경우 이로 인해 발생할 수 있습니다.

첫 번째 진단 단계는 문제가 방정식에 도입된 DRM 암호화 없이 자체적으로 발생하는지 확인하는 것입니다. 콘텐츠를 패키징하려고 하지만 Packager가 내용을 암호화하지 않도록 합니다. 문제가 여전히 있는 경우 컨텐츠를 인코딩하거나 패키지하는 문제 또는 네트워크 인프라의 특정 위치에 문제가 있을 수 있습니다. 암호화 없이 컨텐츠를 패키지할 때 문제가 해결되면 재생 오류가 DRM 문제로 인해 발생할 수 있으며 클라이언트/서버 트리밍에 관여해야 합니다.

Primetime DRM(Primetime Cloud DRM 외부)은 수년 동안 끊임없이 출시되었습니다. Primetime DRM의 문제 해결 및 구성에 대한 다양한 커뮤니티 소스 정보가 있습니다. Adobe은 Primetime DRM(이전의 Adobe 액세스) 사용자를 대상으로 문제와 해결 방법을 집계하고 공유할 수 있는 포럼을 제공했습니다. 이전에 문제가 논의되었는지 확인하려면 다음을 확인하십시오.[https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 클라이언트 오류 트리밍 {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

컨텐츠가 재생되지 않는 경우 발생하는 `DRMErrorEvent`이 기록되는 샘플 비디오 플레이어의 오른쪽 패널을 검사하십시오. 오류 이벤트가 있는 경우 Flash Player 런타임 오류 중 하나와 상관 관계를 맺게 됩니다.

* [DRM 클라이언트 오류 메시지 참조](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages);or
* [AS3 Flash 런타임 오류](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM 문제는 3300부터 시작)


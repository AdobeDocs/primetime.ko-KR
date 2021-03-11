---
description: 때로는 콘텐트를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 이러한 문제가 발생할 수 있습니다.
title: 오류 트리밍 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 트리밍 오류 {#triaging-errors}

때로는 콘텐트를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 이러한 문제가 발생할 수 있습니다.

첫 번째 진단 단계는 문제가 방정식에 도입된 DRM 암호화 없이 자체적으로 발생하는지 확인하는 것입니다. 콘텐츠를 패키징하려고 시도하지만, Packager가 내용을 암호화하지 않도록 합니다. 문제가 여전히 있는 경우 컨텐츠를 인코딩하거나 패키징하는 문제 또는 네트워크 인프라 어딘가에 문제가 있을 수 있습니다. 암호화 없이 컨텐츠를 패키징할 때 문제가 해결되면 DRM 문제로 인해 재생 오류가 발생할 수 있으므로 클라이언트/서버 트리밍에 관여해야 합니다.

Primetime Cloud DRM(Primetime Cloud DRM 제외)은 몇 년 동안 시중에 판매되었습니다. 따라서 Primetime DRM의 문제 해결 및 구성에 대한 다양한 커뮤니티 소스의 정보가 있습니다. Adobe은 Primetime DRM(이전의 Adobe 액세스) 사용자를 대상으로 문제와 해결 방법을 집계 및 공유할 수 있는 포럼을 제공했습니다. 문제가 이전에 논의되었는지 확인하려면 다음을 확인하십시오.[https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 클라이언트 오류 트리밍 {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

내용이 재생되지 않는 경우 발생하는 `DRMErrorEvent`이 기록되는 샘플 비디오 플레이어의 오른쪽 패널을 검사하십시오. 오류 이벤트가 있는 경우 Flash Player 런타임 오류 중 하나와 상관 관계를 맺게 됩니다.

* [DRM 클라이언트 오류 메시지 참조](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages);or
* [AS3 Flash 런타임 오류](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM 문제는 3300부터 시작)


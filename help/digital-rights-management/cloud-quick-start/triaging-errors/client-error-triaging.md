---
description: 경우에 따라 컨텐츠를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 많은 경우 발생할 수 있습니다.
seo-description: 경우에 따라 컨텐츠를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 많은 경우 발생할 수 있습니다.
seo-title: 오류 추적 개요
title: 오류 추적 개요
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 트리밍 오류 {#triaging-errors}

경우에 따라 컨텐츠를 재생할 수 없는 경우도 있습니다. 브라우저 네트워크 스택, 전송 레이어, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 많은 경우 발생할 수 있습니다.

첫 번째 진단 단계는 수식에 도입된 DRM 암호화 없이 문제가 자체적으로 나타나는지 확인하는 것입니다. 콘텐츠를 패키징하려고 하지만, 패키저에서 내용을 암호화하지 않도록 합니다. 문제가 계속 발생하면 컨텐츠를 인코딩하거나 패키징하거나 네트워크 인프라 어딘가에 문제가 있을 수 있습니다. 암호화 없이 컨텐츠를 패키지할 때 문제가 해결되면 DRM 문제로 인해 재생 오류가 발생할 수 있으며 클라이언트/서버 추적에 관여해야 합니다.

Primetime DRM(Primetime Cloud DRM 제외)은 몇 년 동안 시장에 출시되었습니다. 따라서 Primetime DRM의 문제 해결 및 구성에 대한 다양한 커뮤니티 소스 정보가 있습니다. Adobe는 Primetime DRM(이전 Adobe Access) 사용자를 대상으로 문제와 해결 방법을 집계하고 공유할 수 있는 포럼을 제공했습니다. 문제가 이전에 논의되었는지 확인하려면 다음을 확인하십시오. [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 클라이언트 오류 추적 {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

컨텐츠가 재생되지 않는 경우 샘플 비디오 플레이어의 오른쪽 패널을 검사하여 `DRMErrorEvent` 발생하는 모든 것을 기록합니다. 오류 이벤트가 있는 경우 Flash Player 런타임 오류 중 하나와 상호 연관됩니다.

* [DRM 클라이언트 오류 메시지 참조](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages);or
* [AS3 Flash 런타임 오류](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM 문제는 3300부터 시작)


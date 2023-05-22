---
description: 간혹 콘텐츠를 재생할 수 없는 경우가 있습니다. 브라우저 네트워크 스택, 전송 계층, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 다양한 상황이 발생할 수 있습니다.
title: 트리에이징 오류 개요
exl-id: fe94d0a4-4f3c-4b0e-b830-a7a83bac1e85
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 오류 평가 {#triaging-errors}

간혹 콘텐츠를 재생할 수 없는 경우가 있습니다. 브라우저 네트워크 스택, 전송 계층, 운영 체제, Flash Player 런타임 또는 Primetime DRM 시스템의 오류를 포함하여 다양한 상황이 발생할 수 있습니다.

첫 번째 진단 단계는 방정식에 도입된 DRM 암호화 없이 문제가 발현되는지 확인하는 것이다. 콘텐츠를 패키지화하려고 시도하지만, 패키저가 콘텐츠를 암호화하지 않도록 지시합니다. 문제가 여전히 존재하는 경우 콘텐츠를 인코딩하거나 패키징하거나 네트워크 인프라의 어딘가에 문제가 있을 수 있습니다. 콘텐츠가 암호화 없이 패키지화될 때 문제가 해결되면 DRM 문제로 인해 재생 오류가 발생할 수 있으며 클라이언트/서버 트레이징에 참여해야 합니다.

Primetime DRM(Primetime Cloud DRM의 외부)은 몇 년 전부터 시장에 출시되어 왔습니다. 이와 같이 Primetime DRM 문제 해결 및 구성에 대한 풍부한 커뮤니티 소스 정보가 있습니다. Adobe은 Primetime DRM(이전의 Adobe 액세스) 사용자가 문제와 해결 방법을 집계하고 공유할 수 있는 포럼을 제공했습니다. 문제가 이전에 논의되었는지 확인하려면 다음을 확인하십시오. [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 클라이언트 오류 트리에이징 {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

콘텐츠가 재생되지 않는 경우 샘플 비디오 플레이어의 오른쪽 패널을 검사하십시오. 그러면 기록됩니다 `DRMErrorEvent` 그런 경우가 발생합니다. 오류 이벤트가 있으면 Flash Player 런타임 오류 중 하나와 상호 연결됩니다.

* [DRM 클라이언트 오류 메시지 참조](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages); 또는
* [AS3 Flash 런타임 오류](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM 문제는 3300에서 시작)

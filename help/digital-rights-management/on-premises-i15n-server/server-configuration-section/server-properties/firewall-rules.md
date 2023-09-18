---
title: 방화벽 규칙
description: 방화벽 규칙
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 방화벽 규칙{#firewall-rules}

개별화 서버에 대한 액세스를 보호하려면 특정 애플리케이션 경로만 노출하면 됩니다. 개별화 서버는 클라이언트로부터 다음 경로에 대한 요청을 수락해야 합니다.

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

다음과 같은 서비스 경로 [!DNL /flashaccess/admin/*] (즉, 상태 및 관리자 페이지)는 방화벽 내에서만 액세스할 수 있습니다. 방화벽 외부에서 Key Generation Server의 부분에 액세스하면 안 됩니다.

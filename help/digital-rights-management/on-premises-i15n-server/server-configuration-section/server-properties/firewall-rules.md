---
title: 방화벽 규칙
description: 방화벽 규칙
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 방화벽 규칙{#firewall-rules}

개인화 서버에 안전하게 액세스하려면 특정 응용 프로그램 경로만 노출되어야 합니다. 개인화 서버는 클라이언트의 요청을 다음 경로에 수용해야 합니다.

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

[!DNL /flashaccess/admin/*](예: 상태 및 관리 페이지)과 같은 서비스 경로는 방화벽 내에서만 액세스할 수 있어야 합니다. 방화벽 외부에서 키 생성 서버의 어떠한 부분도 액세스할 수 없습니다.

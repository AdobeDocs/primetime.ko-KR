---
seo-title: 방화벽 규칙
title: 방화벽 규칙
uuid: f1629ceb-22de-4bb5-b73f-9b874d97ea8b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 방화벽 규칙{#firewall-rules}

개인화 서버에 안전하게 액세스하려면 특정 응용 프로그램 경로만 노출되어야 합니다. 개인화 서버는 클라이언트의 다음 경로 요청을 승인해야 합니다.

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

[!DNL /flashaccess/admin/*](상태 및 관리 페이지)과 같은 서비스 경로는 방화벽 내에서만 액세스할 수 있어야 합니다. 방화벽 외부에서 키 생성 서버의 어떠한 부분에도 액세스할 수 없습니다.

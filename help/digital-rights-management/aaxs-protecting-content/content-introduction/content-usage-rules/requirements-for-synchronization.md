---
seo-title: 동기화를 위한 요구 사항
title: 동기화를 위한 요구 사항
uuid: 976a0ae1-bece-437e-b95b-6cd222525d13
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 동기화 요구 사항{#requirements-for-synchronization}

클라이언트가 서버와 상태를 동기화할 빈도를 지정합니다. 클라이언트가 대역 외 라이센스를 발급받은 경우(라이센스 서버에 연결하지 않음), 사용 규칙은 클라이언트의 보안 시간과 클라이언트 상태를 서버에 동기화하기 위해 클라이언트가 동기화 메시지를 서버에 전송해야 한다고 지정할 수 있습니다.

동기화 동작은 다음 매개 변수를 사용하여 정의됩니다.

* 시작 간격 — 마지막으로 동기화한 후 다른 동기화 요청을 시작할 때까지 기다리는 시간을 지정합니다.
* 하드 정지 간격 —(선택 사항). 지정된 시간에 동기화가 성공적으로 이루어지지 않으면 재생을 허용하지 않습니다.
* 강제 동기화 확률 — (선택 사항) 클라이언트가 다음 시작 간격 전에 동기화 메시지를 보내야 하는 확률입니다.

>[!NOTE]
>
>이 사용 규칙은 Adobe Access 클라이언트 버전 3.0 이상에서 지원됩니다. 이전 클라이언트의 동작은 라이선스 서버에서 지원하는 최소 클라이언트 버전에 따라 달라집니다. [최소 클라이언트 버전](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)을 참조하십시오.


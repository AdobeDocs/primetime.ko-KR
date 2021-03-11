---
title: 동기화 요청 처리
description: 동기화 요청 처리
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# 동기화 요청 처리 {#handle-synchronization-requests}

라이센스가 동기화 요구 사항 [동기화 요구 사항을 지정하는 경우 클라이언트가 라이센스에 지정된 빈도에 따라 동기화 요청을 주기적으로 서버에 보냅니다. ](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) 동기화 메시지를 활성화하려면 PlayRight에서 `SyncFrequencyRequirements`을(를) 설정합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`입니다.
* 클라이언트 및 서버 지원 프로토콜 버전 5가 모두 지원되는 경우 요청 URL은 &quot;메타데이터의 라이센스 서버 URL:+ &quot; [!DNL /flashaccess/sync/v4]&quot;. 그렇지 않은 경우 요청 URL은 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;입니다.

동기화 메시지는 클라이언트 시간을 서버 시간과 동기화하는 데 사용됩니다. 라이센스가 컨텐츠에 포함되어 있고 라이센스 서버에서 검색할 필요가 없는 경우, 클라이언트가 라이센스 만료를 우회하기 위해 시계를 수정하지 못하도록 하려면 클라이언트의 시간을 동기화하는 것이 중요합니다.

동기화 메시지를 사용하여 롤백 검색을 위해 클라이언트 상태 정보를 서버( `getClientState()`)에 전달할 수도 있습니다.

[롤백 보호](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection)를 참조하십시오.

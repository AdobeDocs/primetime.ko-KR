---
title: 동기화 요청 처리
description: 동기화 요청 처리
copied-description: true
exl-id: bbfc6096-72df-4597-96b3-8f67a640ea8f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 동기화 요청 처리{#handling-synchronization-requests}

. 라이센스에서 동기화 요구 사항([동기화 요구 사항](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization))에서 클라이언트는 라이센스에 지정된 빈도에 따라 동기화 요청을 주기적으로 서버에 전송합니다. 동기화 메시지를 활성화하려면 PlayRight에서 SyncFrequencyRequirements를 설정합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 라이선스 서버 URL: + &quot;/flashaccess/sync/v4&quot;입니다. 그렇지 않으면 요청 URL이 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/sync/v3&quot;입니다.

동기화 메시지는 클라이언트의 시간을 서버의 시간과 동기화하는 데 사용됩니다. 라이센스가 콘텐츠에 포함되어 있고 라이센스 서버에서 검색할 필요가 없는 경우 라이센스 만료를 무시하기 위해 클라이언트가 시계를 수정하지 않도록 클라이언트의 시간을 동기화하는 것이 중요합니다.

동기화 메시지는 클라이언트 상태 정보를 서버에 전달하는 데 사용할 수도 있습니다( `getClientState()`)을 참조하십시오. 다음을 참조하십시오 [롤백 보호](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).

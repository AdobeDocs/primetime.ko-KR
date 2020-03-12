---
seo-title: 동기화 요청 처리
title: 동기화 요청 처리
uuid: 37b2db09-4c09-4216-874b-b570a84569b6
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# 동기화 요청 처리{#handling-synchronization-requests}

. 라이센스가 동기화 요구 사항([동기화 요구 사항](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization))을 지정하는 경우 클라이언트는 라이센스에 지정된 빈도에 따라 동기화 요청을 주기적으로 서버에 보냅니다. 동기화 메시지를 활성화하려면 PlayRight에서 SyncFrequencyRequirements를 설정합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 클라이언트 및 서버 지원 프로토콜 버전 5가 모두 지원되는 경우 요청 URL은 &quot;메타데이터의 라이센스 서버 URL:+ &quot;/flashaccess/sync/v4&quot;. 그렇지 않으면 요청 URL은 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot;/flashaccess/sync/v3&quot;입니다.

동기화 메시지는 클라이언트 시간을 서버 시간과 동기화하는 데 사용됩니다. 라이센스 서버에 라이센스가 포함되어 있고 라이센스 서버에서 검색할 필요가 없는 경우 클라이언트 시간을 동기화하면 클라이언트가 라이센스 만료일을 건너뛰는 데 시간을 변경할 수 없습니다.

동기화 메시지를 사용하여 클라이언트 상태 정보를 서버( `getClientState()`)에 전달하여 롤백 검색을 수행할 수도 있습니다. 롤백 [보호를 참조하십시오](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).
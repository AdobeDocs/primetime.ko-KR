---
seo-title: 개요
title: 개요
uuid: d3bfa65b-2360-4843-b59e-71451fa62a2c
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 개요{#overview}

라이센스를 요청하기 위해 클라이언트는 패키징 중에 컨텐츠에 포함된 메타데이터를 전송합니다. 라이센스 서버는 컨텐츠 메타데이터의 정보를 사용하여 라이센스를 생성합니다.

는 `LicenseHandler` 라이센스 요청을 읽고 요청을 구문 분석합니다. `LicenseHandler`이 기능은 현재 Adobe Access 클라이언트에서 지원되지 `BatchHandlerBase` 않지만 일괄 라이선스 요청을 수용하도록 확장합니다. 이 `getRequests()` 메서드는 `LicenseRequestMessage` 개체 목록을 반환합니다. 호출자는 를 통해 반복해야 `LicenseRequestMessages`하며, 각 요청에 대해 라이센스를 생성하거나 오류 코드를 설정해야 합니다(자세한 내용은 `LicenseRequestMessage` API 참조 설명서 참조). 각 라이센스 요청에 대해 서버에서 라이센스를 발급할지 여부를 결정합니다. 콘텐트 ID, 라이선스 ID 및 정책을 포함하여 콘텐트 메타데이터에서 추출한 정보를 얻으려면 `LicenseRequestMessage.getContentInfo()` 전화 주십시오.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 클라이언트 및 서버 지원 프로토콜 버전 5가 모두 지원되는 경우 요청 URL은 &quot;메타데이터의 라이센스 서버 URL:+ &quot;/flashaccess/license/v4&quot;. 프로토콜 버전 3이 클라이언트 또는 서버에서 지원되는 최대 버전인 경우 Adobe Access 클라이언트는 인증 요청을 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot;/flashaccess/license/v3&quot;로 보냅니다. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot;/flashaccess/license/v1&quot;로 전송됩니다.

요청을 구문 분석하는 동안 오류가 발생하면 `HandlerParsingException` 가 발생합니다. 이 예외에는 클라이언트에 반환되는 오류 정보가 포함됩니다. 오류 정보를 검색하려면 을(를) `HandlerParsingException.getErrorData()`호출합니다. 정책 요구 사항이 충족되지 않아 라이센스를 생성하는 동안 오류가 발생하면 `PolicyEvaluationException` 오류가 발생합니다. 이 예외는 클라이언트로 반환될 `ErrorData` 수도 있습니다. 라이선스 생성 중에 정책을 평가하는 방법에 대한 자세한 내용은 API 설명서를 `LicenseRequestMessage.generateLicense()` 참조하십시오.

라이선스 및 오류는 `LicenseHandler.close()` 호출될 때 한 번에 전송됩니다.

장치에 동일한 컨텐트에 대한 여러 개의 라이선스(동일한 라이선스 ID)가 있을 수 있지만 특정 라이선스 ID 및 정책 ID에 대한 라이선스는 하나만 있을 수 있습니다. 중복된 LicenseID/PolicyID가 있는 라이센스를 받은 경우 새 라이센스의 발행일이 기존 라이센스의 발행일보다 늦은 경우에만 새 라이센스가 이전 라이센스를 대체합니다. 이 로직은 컨텐츠에 포함된 라이선스를 처리하는 데 사용되므로 동일한 정책 ID를 가진 두 개 이상의 라이선스를 컨텐츠 청크에 임베드하는 것이 좋습니다. ActionScript3 API를 통해 클라이언트에 전달되는 라이센스에는 동일한 논리가 `DRMManager.storeVoucher()` 적용됩니다.클라이언트가 이미 나중 발행일에 라이센스를 보유하고 있는 경우 제공된 라이센스가 무시될 수 있습니다.

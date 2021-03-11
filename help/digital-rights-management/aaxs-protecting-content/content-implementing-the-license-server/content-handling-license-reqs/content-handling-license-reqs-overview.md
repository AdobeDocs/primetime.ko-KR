---
title: 개요
description: 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 개요{#overview}

라이센스를 요청하기 위해 클라이언트는 패키징 중에 컨텐츠에 포함된 메타데이터를 전송합니다. 라이센스 서버는 컨텐츠 메타데이터의 정보를 사용하여 라이센스를 생성합니다.

`LicenseHandler`은 라이센스 요청을 읽고 요청을 구문 분석합니다. `LicenseHandler`은(는) 현재 Adobe 액세스 클라이언트 `BatchHandlerBase` 에서 이 기능을 지원하지 않지만, 일괄 처리 라이센스 요청을 수용하도록 확장됩니다. `getRequests()` 메서드는 `LicenseRequestMessage` 개체 목록을 반환합니다. 호출자는 `LicenseRequestMessages`을 반복해야 하며, 각 요청에 대해 라이센스를 생성하거나 오류 코드를 설정해야 합니다(자세한 내용은 `LicenseRequestMessage` API 참조 설명서 참조). 각 라이센스 요청에 대해 서버는 라이센스를 발급할지 여부를 결정합니다. 콘텐트 ID, 라이선스 ID 및 정책을 포함하여 콘텐트 메타데이터에서 추출한 정보를 얻으려면 `LicenseRequestMessage.getContentInfo()`을(를) 호출하십시오.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`입니다.
* 클라이언트 및 서버 지원 프로토콜 버전 5가 모두 지원되는 경우 요청 URL은 &quot;메타데이터의 라이센스 서버 URL:+ &quot;/flashaccess/license/v4&quot;. 프로토콜 버전 3이 클라이언트 또는 서버에서 지원하는 최대값인 경우 Adobe 액세스 클라이언트는 인증 요청을 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot;/flashaccess/license/v3&quot;로 보냅니다. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/license/v1&quot;로 전송됩니다.

요청을 구문 분석하는 동안 오류가 발생하면 `HandlerParsingException`이(가) 발생합니다. 이 예외는 클라이언트에 반환될 오류 정보를 포함합니다. 오류 정보를 검색하려면 `HandlerParsingException.getErrorData()`을(를) 호출합니다. 정책 요구 사항에 맞지 않아 라이선스를 생성하는 동안 오류가 발생하면 `PolicyEvaluationException`이(가) 발생합니다. 이 예외는 클라이언트로 반환되는 `ErrorData`도 포함합니다. 라이선스 생성 중에 정책을 평가하는 방법에 대한 자세한 내용은 `LicenseRequestMessage.generateLicense()`에 대한 API 설명서를 참조하십시오.

`LicenseHandler.close()`이(가) 호출될 때 라이센스 및 오류가 한 번에 전송됩니다.

장치에 동일한 컨텐츠에 대한 여러 개의 라이선스(동일한 라이선스 ID)가 있을 수 있지만 특정 라이센스 ID 및 정책 ID에 대한 하나의 라이선스만 있을 수 있습니다. 중복된 LicenseID/PolicyID로 라이센스를 받은 경우 새 라이센스의 발행일이 기존 라이센스의 발행일보다 늦은 경우에만 새 라이센스가 이전 라이센스를 대체합니다. 이 로직은 컨텐츠에 포함된 라이센스를 처리하는 데 사용되므로 동일한 정책 ID를 가진 두 개 이상의 라이센스를 컨텐츠 청크에 포함하는 것이 좋습니다. 동일한 로직은 `DRMManager.storeVoucher()` ActionScript3 API를 통해 클라이언트에 전달되는 라이선스에 적용됩니다.클라이언트가 이미 나중 발행일에 대한 라이센스를 보유하고 있는 경우 제공된 라이센스를 무시할 수 있습니다.

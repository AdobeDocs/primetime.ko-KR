---
title: 개요
description: 개요
copied-description: true
exl-id: f1a55d5c-c7df-4b8f-8c1e-875d30026069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 개요{#overview}

라이선스를 요청하기 위해 클라이언트는 패키징하는 동안 콘텐츠에 포함된 메타데이터를 전송합니다. 라이선스 서버는 콘텐츠 메타데이터의 정보를 사용하여 라이선스를 생성합니다.

다음 `LicenseHandler` 라이센스 요청을 읽고 요청을 구문 분석합니다. `LicenseHandler`확장 `BatchHandlerBase` 현재 Adobe 액세스 클라이언트가 이 기능을 지원하지 않지만 배치 라이선스 요청을 수용할 수 있습니다. 다음 `getRequests()` 메서드는 다음 목록을 반환합니다. `LicenseRequestMessage` 개체. 호출자는 다음을 반복해야 합니다. `LicenseRequestMessages`, 그리고 각 요청에 대해 라이센스를 생성하거나 오류 코드를 설정합니다( `LicenseRequestMessage` 자세한 내용은 API 참조 설명서 를 참조하십시오.) 각 라이선스 요청에 대해 서버에서 라이선스를 발급할지 여부를 결정합니다. 호출 `LicenseRequestMessage.getContentInfo()` 컨텐츠 ID, 라이선스 ID 및 정책을 포함하여 컨텐츠 메타데이터에서 추출된 정보를 얻습니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 라이선스 서버 URL: + &quot;/flashaccess/license/v4&quot;입니다. 프로토콜 버전 3이 클라이언트 또는 서버에서 지원하는 최대값인 경우 Adobe 액세스 클라이언트는 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/license/v3&quot;에 인증 요청을 전송합니다. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/license/v1&quot;로 전송됩니다.

요청을 구문 분석하는 동안 오류가 발생하는 경우 `HandlerParsingException` 이 throw됩니다. 이 예외에는 클라이언트에 반환할 오류 정보가 포함되어 있습니다. 오류 정보를 검색하려면 `HandlerParsingException.getErrorData()`. 정책 요구 사항이 충족되지 않아 라이센스를 생성하는 도중 오류가 발생하면 `PolicyEvaluationException` 이 throw됩니다. 이 예외에는 다음도 포함됩니다 `ErrorData` 클라이언트로 반환됩니다. 다음에 대한 API 설명서 참조: `LicenseRequestMessage.generateLicense()` 라이선스 생성 중 정책을 평가하는 방법에 대한 자세한 정보.

다음과 같은 경우 라이선스 및 오류가 한 번에 전송됩니다. `LicenseHandler.close()` 이(가) 호출되었습니다.

디바이스에는 동일한 콘텐츠(동일한 라이선스 ID)에 대한 여러 라이선스가 있을 수 있지만 특정 라이선스 ID 및 정책 ID에 대해서는 하나의 라이선스만 있을 수 있습니다. 중복 LicenseID/PolicyID가 있는 라이센스를 받은 경우 새 라이센스의 문제 날짜가 기존 라이센스의 문제 날짜보다 이후인 경우에만 새 라이센스가 이전 라이센스를 대체합니다. 이 논리는 콘텐츠에 포함된 라이선스를 처리하는 데 사용되므로 콘텐츠 청크에 같은 정책 ID를 가진 라이선스를 두 개 이상 포함하는 것은 권장되지 않습니다. 를 통해 클라이언트에 전달되는 라이센스에도 동일한 논리가 적용됩니다. `DRMManager.storeVoucher()` ActionScript3 API; 클라이언트가 나중에 발급하는 날짜가 포함된 라이선스를 이미 보유하고 있는 경우 제공된 라이선스를 무시할 수 있습니다.

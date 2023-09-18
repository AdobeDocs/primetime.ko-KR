---
title: 라이선스 요청 오류 처리
description: 라이선스 요청 오류 처리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 라이선스 요청 오류 처리 {#license-request-error-handling}

요청 구문 분석 중에 오류가 발생하는 경우 `HandlerParsingException` 발생합니다. 이 예외에는 클라이언트에 반환되는 오류 정보가 포함됩니다. 오류 정보를 검색해야 하는 경우 `HandlerParsingException.getErrorData()`. DRM 정책 요구 사항이 충족되지 않아 라이센스를 생성하는 도중 오류가 발생하는 경우 `PolicyEvaluationException` 발생합니다. 이 예외에는 다음도 포함됩니다 `ErrorData` 클라이언트로 반환됩니다.

다음에 대한 API 설명서 참조: `LicenseRequestMessage.generateLicense()` 라이센스 생성 중에 DRM 정책을 평가하는 방법에 대한 자세한 내용.

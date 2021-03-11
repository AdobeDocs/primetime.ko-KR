---
title: 라이선스 요청 오류 처리
description: 라이선스 요청 오류 처리
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 라이선스 요청 오류 처리 {#license-request-error-handling}

요청 구문 분석 중에 오류가 발생하면 `HandlerParsingException`이(가) 발생합니다. 이 예외는 클라이언트에 반환되는 오류 정보를 포함합니다. 오류 정보를 검색해야 하는 경우 `HandlerParsingException.getErrorData()`을(를) 호출해야 합니다. DRM 정책 요구 사항이 충족되지 않아 라이선스를 생성하는 동안 오류가 발생하면 `PolicyEvaluationException`이(가) 발생합니다. 이 예외는 클라이언트로 반환되는 `ErrorData`도 포함합니다.

라이선스 생성 중 DRM 정책이 평가되는 방법에 대한 자세한 내용은 `LicenseRequestMessage.generateLicense()`에 대한 API 설명서를 참조하십시오.

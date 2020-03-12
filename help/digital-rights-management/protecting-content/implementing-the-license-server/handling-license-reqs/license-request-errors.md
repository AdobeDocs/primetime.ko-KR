---
seo-title: 라이선스 요청 오류 처리
title: 라이선스 요청 오류 처리
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이선스 요청 오류 처리 {#license-request-error-handling}

요청 구문 분석 중에 오류가 발생하면 오류가 `HandlerParsingException` 발생합니다. 이 예외는 클라이언트에 반환되는 오류 정보를 포함합니다. 오류 정보를 검색해야 하는 경우 전화해야 `HandlerParsingException.getErrorData()`합니다. DRM 정책 요구 사항이 충족되지 않아 라이센스를 생성하는 동안 오류가 발생하면 오류가 `PolicyEvaluationException` 발생합니다. 이 예외는 클라이언트로 반환될 `ErrorData` 수도 있습니다.

라이선스 생성 중 DRM 정책을 평가하는 방법에 대한 자세한 내용은 API 설명서를 `LicenseRequestMessage.generateLicense()` 참조하십시오.

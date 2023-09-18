---
description: Adobe 비디오 엔진의 암호화 모듈은 NATIVE_ERROR 메타데이터 개체에서 이러한 알림을 반환합니다.
title: NATIVE_ERROR 암호화 값
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 8%

---

# NATIVE_ERROR: 암호화 값{#native-error-crypto-values}

Adobe 비디오 엔진의 암호화 모듈은 NATIVE_ERROR 메타데이터 개체에서 이러한 알림을 반환합니다.

| NATIVE_ERROR_CODE 메타데이터 키 값 | NATIVE_ERROR_NAME 메타데이터 키 값 | 의미 |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 사용 중인 알고리즘이 지원되지 않습니다. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 데이터가 손상되었습니다. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 버퍼가 너무 작습니다. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 잘못된 인증서. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 다이제스트 업데이트. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 다이제스트 완료. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 잘못된 매개변수. |

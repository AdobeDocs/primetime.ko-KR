---
description: Adobe 비디오 엔진의 암호화 모듈은 NATIVE_ERROR 메타데이터 객체에 이러한 알림을 반환합니다.
title: NATIVE_ERROR 암호화 값
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 8%

---


# NATIVE_ERROR:암호화 값{#native-error-crypto-values}

Adobe 비디오 엔진의 암호화 모듈은 NATIVE_ERROR 메타데이터 객체에 이러한 알림을 반환합니다.

| NATIVE_ERROR_CODE 메타데이터 키 값 | NATIVE_ERROR_NAME 메타데이터 키의 값 | 의미 |
|---|---|---|
| 300년 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 사용 중인 알고리즘은 지원되지 않습니다. |
| 301년 | `CRYPTO_ERROR_CORRUPTED_DATA` | 데이터가 손상되었습니다. |
| 302년 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 버퍼가 너무 작습니다. |
| 303년 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 인증서가 잘못되었습니다. |
| 304년 | `CRYPTO_ERROR_DIGEST_UPDATE` | 다이제스트 업데이트. |
| 305년 | `CRYPTO_ERROR_DIGEST_FINISH` | 다이제스트 완료 |
| 306년 | `CRYPTO_ERROR_BAD_PARAMETER` | 매개 변수가 잘못되었습니다. |


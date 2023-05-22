---
title: Xbox Live XSTS 토큰 유효성 검사
description: Xbox Live XSTS 토큰 유효성 검사
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Xbox Live XSTS 토큰 유효성 검사{#xbox-live-xsts-token-validation}

XSTS 요청의 경우 `customerSpecificAuthToken` 필드에는 Base64로 인코딩된 XSTS 토큰이 포함됩니다. 샘플 `XSTSValidator` 코드는 Base64 디코딩 토큰을 검사하여 `EncryptedAssertion` 요소. 그러나 다른 방법을 사용하여 이러한 요청과 Xbox 이외의 요청을 구분할 수 있습니다. 예를 들어 다른 URL을 사용할 수 있습니다.

응답 메시지에서 반환된 정책은 Xbox 키 요청과 함께 제공된 DRM 메타데이터의 원래 정책을 덮어씁니다. Xbox 클라이언트는 일부 정책 기능만 지원하며 이 필드만 원래 정책을 무효화합니다.

토큰 암호 해독 및 유효성 검사를 지원하는 데 필요한 추가 설정 단계가 있습니다. 다음을 로드해야 합니다. [!DNL xsts_partner_cert.pfx] 및 [!DNL x_secure_token_service.part.xboxlive.com.cer] 자격 증명을 JKS 형식 키 저장소로 가져와서 백엔드 권한 부여 서버에 시스템 속성으로 제공합니다 `xsts-keystore`. 기본적으로 파트너는 [!DNL .pfx] 에 별칭이 있습니다. `xsts`, 토큰 유효성 검사 인증서에 별칭이 있음 `xsts-verify-cert`. 시스템 속성을 사용하여 재정의할 수도 있습니다. 마지막으로 시스템 속성이 있습니다 `xsts-keystore-password` 에는 기본값이 없으며 키 저장소 암호가 포함되어 있습니다. 에서 읽는 시스템 속성 `XSTSValidator` 코드는 아래에 요약되어 있습니다.

| 시스템 속성 | 기본값 | 댓글 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 유효성 검사기에서 사용하는 JKS 형식 키 저장소입니다. |
| `xsts-keystore-password` |  | 키 저장소의 암호 |
| `xsts-alias` | `xsts` | 키 저장소에서 암호 해독 키를 검색하는 데 사용되는 앨리어스 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 키 저장소에서 유효성 검사 인증서를 검색하는 데 사용되는 앨리어스 |


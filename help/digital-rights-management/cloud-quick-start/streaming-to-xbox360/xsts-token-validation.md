---
seo-title: Xbox Live XSTS 토큰 유효성 검사
title: Xbox Live XSTS 토큰 유효성 검사
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Xbox Live XSTS 토큰 유효성 검사{#xbox-live-xsts-token-validation}

XSTS 요청의 경우 `customerSpecificAuthToken` 필드에 Base64 인코딩 XSTS 토큰이 포함됩니다. 샘플 `XSTSValidator` 코드는 Base64 디코딩된 토큰을 검사하여 `EncryptedAssertion` 요소가 있는지 확인합니다.그러나 다른 방법을 사용하여 이러한 요청과 Xbox가 아닌 요청을 구분할 수 있습니다. 예를 들어 다른 URL을 사용할 수 있습니다.

응답 메시지에서 반환된 정책은 Xbox 키 요청과 함께 제공된 DRM 메타데이터의 원래 정책을 덮어씁니다. Xbox 클라이언트는 정책 기능의 하위 집합만 지원되며, 이 필드만 원래의 정책을 재정의할 수 있습니다.

토큰 암호 해독 및 유효성 검사를 지원하는 데 필요한 추가 설정 단계가 있습니다. JKS 형식 키 저장소에 [!DNL xsts_partner_cert.pfx] 및 [!DNL x_secure_token_service.part.xboxlive.com.cer] 자격 증명을 로드해야 합니다. 그러면 백엔드 자격 부여 서버에 시스템 속성으로 제공할 수 `xsts-keystore`있습니다. 기본적으로 파트너는 [!DNL .pfx] 별칭을 `xsts`가지며 토큰 유효성 검사 인증서에 별칭이 `xsts-verify-cert`있습니다. 시스템 속성을 사용하여 이러한 설정을 재정의할 수도 있습니다. 마지막으로, 기본값이 `xsts-keystore-password` 없고 키 저장소 암호가 포함된 시스템 속성이 있습니다. 코드가 읽는 시스템 속성은 `XSTSValidator` 아래에 요약되어 있습니다.

| 시스템 속성 | 기본값 | 주석 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 유효성 검사기에서 사용하는 JKS 형식 키 저장소입니다. |
| `xsts-keystore-password` |  | 키 저장소 암호 |
| `xsts-alias` | `xsts` | 키 저장소에서 암호 해독 키를 검색하는 데 사용되는 별칭 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 키 저장소에서 유효성 검사 인증서를 검색하는 데 사용되는 별칭 |


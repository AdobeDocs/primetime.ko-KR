---
seo-title: 인증서 서명 요청 생성(요청자)
title: 인증서 서명 요청 생성(요청자)
uuid: 04abd5d2-77ac-4f89-8bea-31d389159aee
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# 인증서 서명 요청 생성(요청자) {#generate-a-certificate-signing-request-requester}

1. 키 쌍을 생성합니다. OpenSSL과 같은 유틸리티를 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe에서는 키 이름에 인증서 유형(lic, pkgr, trans, 시험버전 또는 eval)을 포함하는 것이 좋습니다. 이 명명 규칙을 사용하면 라이센스 서버에 배포할 때 더 쉽게 배포할 수 있습니다. 이 예에서는 &quot;mycompany-license.key&quot;를 사용합니다. 평가 및 시험버전의 경우 &quot;mycompany-eval.key&quot; 및 &quot;mycompany-trial.key&quot;를 사용하십시오.

1. 개인 키를 보호할 암호를 입력합니다.

   암호는 12자 이상이어야 합니다. 대문자와 소문자를 혼합하여 사용해야 합니다. OpenSSL을 사용하여 강력한 암호를 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl rand -base64 8
   ```

1. CSR 파섹

   OpenSSL을 사용하여 CSR을 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. 개인 키에 대한 암호를 입력하라는 메시지가 표시됩니다.
1. 개인 키 및 암호 백업 복사본을 만듭니다.

   개인 키가 손실되었거나 손상된 경우 Adobe 인증서 관리자에게 문의하여 인증서를 취소하고 새 키를 요청하십시오.

   >[!NOTE]
   >
   >HSM을 사용하여 개인 키와 암호를 보호하는 것이 좋습니다.


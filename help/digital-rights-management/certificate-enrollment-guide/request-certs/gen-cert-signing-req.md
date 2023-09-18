---
title: 인증서 서명 요청 생성(요청자)
description: 인증서 서명 요청 생성(요청자)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 인증서 서명 요청 생성(요청자) {#generate-a-certificate-signing-request-requester}

1. 키 쌍을 생성합니다. OpenSSL과 같은 유틸리티를 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe은 키 이름에 인증서 유형(lic, pkgr, trans, trial 또는 eval)을 포함할 것을 권장합니다. 이러한 명명 규칙을 사용하면 라이선스 서버에 보다 쉽게 배포할 수 있습니다. 이 예에서는 &quot;mycompany-license.key&quot;를 사용합니다. 평가 및 체험판 버전의 경우 &quot;mycompany-eval.key&quot; 및 &quot;mycompany-trial.key&quot;를 사용합니다.

1. 개인 키를 보호하려면 암호를 입력하십시오.

   암호는 12자 이상이어야 합니다. 문자에는 대문자 및 소문자 ASCII 문자와 숫자를 혼합해야 합니다. OpenSSL을 사용하여 강력한 암호를 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl rand -base64 8
   ```

1. CSR(인증서 서명 요청)을 생성합니다.

   OpenSSL을 사용하여 CSR을 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. 개인 키의 암호를 입력하라는 메시지가 표시됩니다.
1. 개인 키 및 암호의 백업 사본을 만듭니다.

   개인 키를 분실하거나 훼손된 경우 Adobe 인증서 관리자에게 문의하여 인증서를 해지하고 새 인증서를 요청하십시오.

   >[!NOTE]
   >
   >Adobe은 개인 키와 암호를 보호하기 위해 HSM을 사용할 것을 권장합니다.

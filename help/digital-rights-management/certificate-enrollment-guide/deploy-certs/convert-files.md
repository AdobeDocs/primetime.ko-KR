---
title: 파일 변환
description: 파일 변환
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 파일 변환{#convert-files}

요청자가 OpenSSL 및 개인 키와 같은 유틸리티를 사용하여 명령 창에서 다음 명령을 입력하여 PKCS#12(pfx) 및 PEM/DER 파일을 생성합니다.

1. PKCS#7 파일을 임시 PEM 파일로 변환합니다.

   OpenSSL을 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >이 임시 PEM에는 중간 CA에 대한 인증서와 인증서가 포함되어 있습니다. 이러한 인증서를 사용하여 PFX 파일을 생성합니다.

1. 임시 PEM 파일을 PFX 파일로 변환합니다.

   OpenSSL을 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. 임시 PEM 파일을 최종 PEM 파일로 변환합니다.

   OpenSSL을 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >필수 사항은 아니지만 개인 키(private_key_password) 및 PFX(pfx_password)에 다른 암호를 사용하는 것이 좋습니다.

   이 최종 PEM 파일에는 인증서만 포함되어 있습니다.

1. PEM 파일을 DER 파일로 변환합니다.

   OpenSSL을 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >DER 파일은 HTTP Dynamic Streaming 패키저에만 필요합니다.


---
title: 도메인 CA 인증서 가져오기
description: 도메인 CA 인증서 가져오기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 도메인 CA 인증서 가져오기{#obtain-domain-ca-certificates}

라이센스 서버, 패키지 또는 전송 인증서와 달리 도메인 CA 인증서는 Adobe을 통해 발급되지 않습니다. 인증 기관에서 이 인증서를 얻거나 이 용도로 사용할 자체 서명된 인증서를 생성할 수 있습니다.

도메인 CA 인증서는 1024비트 키를 사용해야 하며 CA 인증서에 필요한 표준 특성을 포함해야 합니다.

* CA 플래그가 true로 설정된 기본 제한 확장
* 인증서 서명을 지정하는 키 사용 확장이 허용됨

예를 들어, OpenSSL을 사용하여 자체 서명된 CA 인증서를 다음과 같이 생성할 수 있습니다.

1. 다음을 포함하는 [!DNL ca-extensions.txt]라는 파일을 만듭니다.

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. 키 생성:

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. CSR 생성:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. 인증서 생성:

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. 암호 생성:

   ```
   openssl rand -base64 8 
   ```

1. PFX 생성:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```


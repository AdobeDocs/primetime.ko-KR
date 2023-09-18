---
title: 도메인 CA 인증서 받기
description: 도메인 CA 인증서 받기
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 도메인 CA 인증서 받기{#obtain-domain-ca-certificates}

License Server, Packager 또는 Transport 인증서와 달리 Domain CA 인증서는 Adobe에서 발급하지 않습니다. 인증 기관에서 이 인증서를 받거나 이 용도로 사용할 자체 서명된 인증서를 생성할 수 있습니다.

도메인 CA 인증서는 1024비트 키를 사용하고 CA 인증서에 필요한 표준 속성을 포함해야 합니다.

* CA 플래그가 true로 설정된 기본 제약 조건 확장
* 인증서 서명을 지정하는 키 사용 확장이 허용됩니다.

예를 들어 OpenSSL을 사용하여 다음과 같이 자체 서명된 CA 인증서를 생성할 수 있습니다.

1. 라는 파일 만들기 [!DNL ca-extensions.txt] 포함:

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

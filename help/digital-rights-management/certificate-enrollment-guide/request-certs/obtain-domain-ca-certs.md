---
seo-title: 도메인 CA 인증서 얻기
title: 도메인 CA 인증서 얻기
uuid: 41bbe02b-363a-47f4-9cc0-350730b6c787
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# 도메인 CA 인증서 얻기{#obtain-domain-ca-certificates}

라이센스 서버, 패키지 또는 전송 인증서와 달리 도메인 CA 인증서는 Adobe에서 발행하지 않습니다. 인증 기관에서 이 인증서를 얻거나 이러한 목적으로 사용할 자체 서명 인증서를 생성할 수 있습니다.

도메인 CA 인증서는 1024비트 키를 사용하고 CA 인증서에 필요한 표준 특성을 포함해야 합니다.

* CA 플래그가 true로 설정된 기본 제한 확장
* 인증서 서명을 지정하는 키 사용 확장이 허용됨

예를 들어 OpenSSL을 사용하면 다음과 같이 자체 서명된 CA 인증서를 생성할 수 있습니다.

1. 다음을 [!DNL ca-extensions.txt] 포함하는 파일을 만듭니다.

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


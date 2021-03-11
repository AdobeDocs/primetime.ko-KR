---
title: XSTS 유효성 검사기용 JKS 만들기
description: XSTS 유효성 검사기용 JKS 만들기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# XSTS 유효성 검사기용 JKS 만들기{#create-jks-for-an-xsts-validator}

1. 파트너 [!DNL .pfx] 파일에 있는 개인 인증서의 별칭 이름을 확인합니다.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. [!DNL .pfx]을(를) [!DNL .jks](으)로 변환합니다.

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   여기서 `<alias>`은 1단계에서 발견한 개인 인증서의 별칭 이름입니다.
1. [!DNL x_secure_token_service.part.xboxlive.com.cer]을(를) 가져옵니다.

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. [!DNL xsts.jks]을(를) Tomcat 홈 디렉토리에 배치하고 Tomcat에 대해 `-Dxsts-keystore-password=****`을 정의합니다.

[!DNL xsts_partner_cert.pfx] 및 [!DNL xsts.jks]에서 다른 암호를 사용하는 경우 `jks`에서 `xsts` 암호를 업데이트하여 동일하게 만듭니다.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```

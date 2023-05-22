---
title: XSTS 유효성 검사기에 대한 JKS 만들기
description: XSTS 유효성 검사기에 대한 JKS 만들기
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# XSTS 유효성 검사기에 대한 JKS 만들기{#create-jks-for-an-xsts-validator}

1. Partner에 있는 Private Cert의 별칭 이름 확인 [!DNL .pfx] 파일.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 전환 [!DNL .pfx] 끝 [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (여기서 `<alias>` 는 1단계에서 검색한 비공개 인증서의 별칭 이름입니다.)
1. 가져오기 [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] Tomcat 홈 디렉터리에서 다음을 정의합니다. `-Dxsts-keystore-password=****` Tomcat용

If [!DNL xsts_partner_cert.pfx] 및 [!DNL xsts.jks] 다른 암호를 사용하고 있습니다. `xsts` 의 암호 `jks` 그들을 같게 만들려고.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```

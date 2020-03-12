---
seo-title: XSTS 유효성 검사기용 JKS 만들기
title: XSTS 유효성 검사기용 JKS 만들기
uuid: e02b517d-0b72-4e95-92b2-09b8f785cce6
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# XSTS 유효성 검사기용 JKS 만들기{#create-jks-for-an-xsts-validator}

1. 파트너 [!DNL .pfx] 파일에 있는 개인 인증서의 별칭 이름을 확인합니다.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 변환 [!DNL .pfx] 대상 [!DNL .jks]

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (여기서 `<alias>` 는 1단계에서 발견한 개인 인증서의 별칭 이름입니다.)
1. 가져오기를 [!DNL x_secure_token_service.part.xboxlive.com.cer]참조하십시오.

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Tomcat 홈 [!DNL xsts.jks] 디렉토리에 넣고 Tomcat에 `-Dxsts-keystore-password=****` 대해 정의합니다.

다른 암호를 [!DNL xsts_partner_cert.pfx] 사용하고 [!DNL xsts.jks] 있는 경우 암호를 `xsts` 업데이트하여 암호를 동일하게 `jks` 만듭니다.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```

---
description: HSM을 선택하여 서버 자격 증명을 저장하는 경우 HSM에 개인 키 및 인증서를 로드하고 pkcs11.cfg 구성 파일을 생성해야 합니다.
seo-description: HSM을 선택하여 서버 자격 증명을 저장하는 경우 HSM에 개인 키 및 인증서를 로드하고 pkcs11.cfg 구성 파일을 생성해야 합니다.
seo-title: HSM 구성
title: HSM 구성
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM 구성{#hsm-configuration}

HSM을 선택하여 서버 자격 증명을 저장하는 경우 HSM에 개인 키 및 인증서를 로드하고 pkcs11.cfg 구성 파일을 생성해야 합니다.

LicenseServer.ConfigRoot *디렉토리에서 구성 파일을 찾아야* 합니다.

PKCS11 구성 파일의 예는 Adobe Primetime DRM DVD의 [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] 디렉토리를 참조하십시오.

파일 형식에 대한 자세한 내용은 Sun PKCS11 공급자 설명서를 [!DNL pkcs11.cfg] 참조하십시오.

파일이 있는 디렉토리(Java JRE 및 JDK와 함께 [!DNL pkcs11.cfg] [!DNL keytool] 설치)에서 다음 명령을 사용하여 HSM 및 Sun PKCS11 구성 파일이 올바르게 구성되었는지 확인할 수 있습니다.

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에서 자격 증명을 볼 수 있는 경우 HSM이 올바르게 구성되고 라이센스 서버가 자격 증명을 액세스할 수 있습니다.

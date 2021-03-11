---
description: 서버 자격 증명을 저장할 HSM을 선택하는 경우 전용 키와 인증서를 HSM에 로드하고 pkcs11.cfg 구성 파일을 생성해야 합니다.
title: HSM 구성
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# HSM 구성{#hsm-configuration}

서버 자격 증명을 저장할 HSM을 선택하는 경우 전용 키와 인증서를 HSM에 로드하고 pkcs11.cfg 구성 파일을 생성해야 합니다.

*LicenseServer.ConfigRoot* 디렉토리에서 구성 파일을 찾아야 합니다.

PKCS11 구성 파일의 예제는 Adobe Primetime DRM DVD의 [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] 디렉토리를 참조하십시오.

[!DNL pkcs11.cfg] 파일의 형식에 대한 Sun PKCS11 공급자 설명서를 참조하십시오.

[!DNL pkcs11.cfg] 파일이 있는 디렉토리에서 다음 명령을 사용하여 HSM 및 Sun PKCS11 구성 파일이 올바르게 구성되었는지 확인할 수 있습니다( [!DNL keytool] Java JRE 및 JDK와 함께 설치).

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에서 자격 증명을 볼 수 있는 경우 HSM이 올바르게 구성되고 라이센스 서버가 자격 증명을 액세스할 수 있습니다.

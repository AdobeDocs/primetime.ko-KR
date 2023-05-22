---
description: 서버 자격 증명을 저장할 HSM을 선택하는 경우 HSM에 개인 키와 인증서를 로드하고 pkcs11.cfg 구성 파일을 생성해야 합니다.
title: HSM 구성
exl-id: 4c4423ea-b7af-4a30-99ac-f5b74a1e1168
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# HSM 구성{#hsm-configuration}

서버 자격 증명을 저장할 HSM을 선택하는 경우 HSM에 개인 키와 인증서를 로드하고 pkcs11.cfg 구성 파일을 생성해야 합니다.

에서 구성 파일을 찾아야 합니다. *LicenseServer.ConfigRoot* 디렉토리.

다음을 참조하십시오. [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] Adobe Primetime DRM DVD의 디렉토리(예: PKCS11 구성 파일).

의 형식에 대해서는 Sun PKCS11 공급자 설명서를 참조하십시오. [!DNL pkcs11.cfg] 파일.

다음 명령을 사용할 수 있습니다. [!DNL pkcs11.cfg] 파일이 있습니다( [!DNL keytool] 는 Java JRE 및 JDK와 함께 설치되어 HSM 및 Sun PKCS11 구성 파일이 올바르게 구성되었는지 확인합니다.

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에서 자격 증명을 볼 수 있는 경우 HSM이 올바르게 구성되며 라이센스 서버가 이제 자격 증명에 액세스할 수 있습니다.

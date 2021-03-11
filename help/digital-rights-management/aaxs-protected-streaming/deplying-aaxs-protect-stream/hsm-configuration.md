---
title: HSM 구성
description: HSM 구성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# HSM 구성 {#hsm-configuration}

HSM을 사용하여 서버 자격 증명을 저장하도록 선택한 경우 개인 키와 인증서를 HSM에 로드하고 [!DNL pkcs11.cfg] 구성 파일을 생성해야 합니다. 이 파일은 *LicenseServer.ConfigRoot* 디렉토리에 있어야 합니다. PKCS11 구성 파일의 예제는 Adobe 액세스 DVD의 [!DNL Adobe Access Server for Protected Streaming/configs] 디렉토리를 참조하십시오. [!DNL pkcs11.cfg] 형식에 대한 자세한 내용은 Sun PKCS11 공급자 설명서를 참조하십시오.

HSM 및 Sun PKCS11 구성 파일이 제대로 구성되어 있는지 확인하려면 [!DNL pkcs11.cfg] 파일이 있는 디렉토리에서 다음 명령을 사용할 수 있습니다( [!DNL keytool] 가 Java JRE 및 JDK와 함께 설치됨).

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에 자격 증명이 표시되면 HSM이 제대로 구성되고 라이센스 서버가 자격 증명을 액세스할 수 있습니다.

>[!NOTE]
>
>보호 스트리밍을 위한 Adobe 액세스 서버는 현재 64비트 Windows OS에서 HSM을 지원하지 않습니다.

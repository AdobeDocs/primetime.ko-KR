---
title: HSM 구성
description: HSM 구성
copied-description: true
exl-id: a3e5759e-1419-4519-bcd7-de83364a48f8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# HSM 구성 {#hsm-configuration}

HSM을 사용하여 서버 자격 증명을 저장하기로 선택한 경우 HSM에 개인 키와 인증서를 로드하고 [!DNL pkcs11.cfg] 구성 파일입니다. 이 파일은 다음 위치에 있어야 합니다. *LicenseServer.ConfigRoot* 디렉토리. 다음을 참조하십시오. [!DNL Adobe Access Server for Protected Streaming/configs] Adobe Access DVD의 디렉터리입니다. 형식에 대한 자세한 내용은 [!DNL pkcs11.cfg]Sun PKCS11 공급자 설명서를 참조하십시오.

HSM 및 Sun PKCS11 구성 파일이 제대로 구성되어 있는지 확인하려면 [!DNL pkcs11.cfg] 파일이 있습니다( [!DNL keytool] 는 Java JRE 및 JDK와 함께 설치됩니다).

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에 자격 증명이 표시되면 HSM이 제대로 구성되고 라이선스 서버가 자격 증명에 액세스할 수 있습니다.

>[!NOTE]
>
>보호된 스트리밍용 Adobe 액세스 서버는 현재 64비트 Windows OS에서 HSM을 지원하지 않습니다.

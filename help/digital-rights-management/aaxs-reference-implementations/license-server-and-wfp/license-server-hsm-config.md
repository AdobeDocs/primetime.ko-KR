---
title: HSM 구성
description: HSM 구성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# HSM 구성 {#hsm-configuration}

HSM을 사용할 필요는 없지만 권장됩니다. HSM 지원을 위한 Sun PKCS11 공급자를 사용하도록 참조 구현을 구성할 수 있습니다. HSM에서 자격 증명을 사용하려면 Sun PKCS11 공급자에 대한 구성 파일을 생성해야 합니다. 자세한 내용은 Sun 설명서를 참조하십시오. HSM 및 Sun PKCS11 구성 파일이 제대로 구성되어 있는지 확인하려면 다음 명령을 사용할 수 있습니다(키 도구는 Java JDK와 함께 설치됨).

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

목록에 자격 증명이 표시되면 HSM이 제대로 구성됩니다.

>[!NOTE]
>
>Java 1.7부터 Windows용 64비트 Sun Java는 HSM 장치와 통신하기 위해 Adobe Access DRM에 필요한 PKCS11 인터페이스를 지원하지 않습니다. HSM을 사용하려는 경우 32비트 버전의 Java를 사용하거나 전체 PKCS11 인터페이스를 지원하는 JDK를 사용하십시오.


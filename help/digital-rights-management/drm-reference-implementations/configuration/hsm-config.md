---
description: HSM을 지원하는 Sun PKCS#11 공급자를 통해 참조 구현을 구성할 수 있습니다. HSM을 사용할 필요는 없지만 사용하는 것이 좋습니다.
title: HSM 구성
exl-id: 87a7d242-8202-4749-91a6-e6697be6a61d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# HSM 구성{#hsm-configuration}

HSM을 지원하는 Sun PKCS#11 공급자를 통해 참조 구현을 구성할 수 있습니다. HSM을 사용할 필요는 없지만 사용하는 것이 좋습니다.

HSM에서 자격 증명을 사용하려면 Sun PKCS#11 공급자에 대한 구성 파일을 생성해야 합니다. 자세한 내용은 [Java PCKS#11 참조 안내서](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

HSM 및 Sun PKCS#11 구성 파일이 구성되어 있는지 확인하려면 Java JDK와 함께 설치된 키 도구를 사용하여 다음 명령을 입력합니다.

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에서 자격 증명을 볼 수 있는 경우 HSM을 올바르게 구성했습니다.

>[!NOTE]
>
>Java 1.7부터 64비트 Windows용 Sun Java는 Adobe Primetime DRM이 HSM 장치와 통신하는 데 필요한 PKCS#11 인터페이스를 더 이상 지원하지 않습니다. HSM을 사용할 계획이라면 32비트 버전의 Java를 사용하거나 전체 PKCS#11 인터페이스를 지원하는 JDK를 사용해야 합니다.

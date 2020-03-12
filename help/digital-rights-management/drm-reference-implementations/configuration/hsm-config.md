---
description: HSM을 지원하는 Sun PKCS#11 공급자를 사용하여 참조 구현을 구성할 수 있습니다. HSM을 사용할 필요는 없지만 권장됩니다.
seo-description: HSM을 지원하는 Sun PKCS#11 공급자를 사용하여 참조 구현을 구성할 수 있습니다. HSM을 사용할 필요는 없지만 권장됩니다.
seo-title: HSM 구성
title: HSM 구성
uuid: 2741ac40-aa42-4aa7-9864-037f3ed3dee2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM 구성{#hsm-configuration}

HSM을 지원하는 Sun PKCS#11 공급자를 사용하여 참조 구현을 구성할 수 있습니다. HSM을 사용할 필요는 없지만 권장됩니다.

HSM에서 자격 증명을 사용하려면 Sun PKCS#11 공급자에 대한 구성 파일을 생성해야 합니다. 자세한 내용은 Java PCKS# [11 참조 안내서를 참조하십시오](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

HSM 및 Sun PKCS#11 구성 파일이 구성되어 있는지 확인하려면 Java JDK와 함께 설치된 키 도구를 사용하여 다음 명령을 입력합니다.

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에서 자격 증명을 볼 수 있는 경우 HSM을 올바르게 구성했습니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Java 1.7부터 Windows용 64비트 Sun Java는 Adobe Primetime DRM이 HSM 디바이스와 통신하는 데 필요한 PKCS#11 인터페이스를 더 이상 지원하지 않습니다. HSM을 사용하려는 경우 32비트 버전의 Java를 사용하거나 전체 PKCS#11 인터페이스를 지원하는 JDK를 사용해야 합니다.


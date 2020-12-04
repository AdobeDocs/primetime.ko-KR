---
description: Password Scrambler 유틸리티는 보호된 스트리밍 구성 파일을 위한 Adobe Primetime DRM Server의 암호를 암호화합니다.
seo-description: Password Scrambler 유틸리티는 보호된 스트리밍 구성 파일을 위한 Adobe Primetime DRM Server의 암호를 암호화합니다.
seo-title: 암호 스크램블러
title: 암호 스크램블러
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---


# 암호 스크램블러 {#password-scrambler}

Password Scrambler 유틸리티는 보호된 스트리밍 구성 파일을 위한 Adobe Primetime DRM Server의 암호를 암호화합니다.

scrambler를 실행하려면 다음을 입력합니다.

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

or

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

이 유틸리티는 다음 메시지를 표시합니다.

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

[!DNL flashaccess-global.xml] 및 [!DNL flashaccess-tenant.xml] 파일에서 지정한 모든 암호는 암호화되어야 합니다.

>[!NOTE]
>
>보호된 스트리밍을 위한 Primetime DRM Server의 암호 스크램블러 유틸리티는 참조 구현 라이선스 서버와 함께 제공되는 스크램블러와 호환되지 않습니다.
---
title: 암호 스크램블러
description: 암호 스크램블러
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# 암호 스크램블러 {#password-scrambler}

Password Scrambler 유틸리티는 암호를 암호화하여 보호된 스트리밍 구성 파일의 Adobe Access Server에서 사용할 수 있도록 합니다. scrambler를 실행하려면 명령을 실행합니다.

```
Scrambler.bat password 
```

또는 명령:

```
java -jar libs/flashaccess-scrambler.jar password  
```

이 유틸리티는 다음 메시지를 출력합니다.

```
Encrypted password: scrambled-password 
```

flashaccess-global.xml 및 flashaccess-tenant.xml에 지정된 모든 암호는 암호화되어야 합니다.

>[!NOTE]
>
>보호 스트리밍을 위한 Adobe Access Server의 암호 스크램블러 유틸리티는 참조 구현 라이센스 서버에 제공된 scrambler와 상호 대체할 수 없습니다.


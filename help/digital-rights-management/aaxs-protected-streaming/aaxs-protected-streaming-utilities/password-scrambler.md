---
title: 암호 스크램블러
description: 암호 스크램블러
copied-description: true
exl-id: ceedd61e-918b-453f-8d21-628b2d8713ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 암호 스크램블러 {#password-scrambler}

암호 스크램블러 유틸리티는 Adobe Access Server for Protected Streaming 구성 파일에서 사용할 수 있도록 암호를 암호화합니다. 스크램블러를 실행하려면 다음 명령을 실행합니다.

```
Scrambler.bat password 
```

또는 명령:

```
java -jar libs/flashaccess-scrambler.jar password  
```

유틸리티는 다음 메시지를 출력합니다.

```
Encrypted password: scrambled-password 
```

flashaccess-global.xml 및 flashaccess-tenant.xml에 지정된 모든 암호를 암호화해야 합니다.

>[!NOTE]
>
>Protected Streaming용 Adobe Access Server의 암호 스크램블러 유틸리티는 참조 구현 라이선스 서버와 함께 제공되는 스크램블러와 호환되지 않습니다.

---
seo-title: 암호 스크램블러
title: 암호 스크램블러
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# 암호 스크램블러 {#password-scrambler}

Password Scrambler 유틸리티는 암호를 암호화하여 Protected Streaming 구성 파일을 위해 Adobe Access Server에서 사용할 수 있도록 합니다. scrambler를 실행하려면 명령을 실행합니다.

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

flashaccess-global.xml 및 flashaccess-tenant.xml에 지정된 모든 암호는 암호화해야 합니다.

>[!NOTE]
>
>보호 스트리밍을 위한 Adobe Access Server의 암호 스크램블러 유틸리티는 Reference Implementation License Server와 함께 제공되는 scrambler와 호환되지 않습니다.


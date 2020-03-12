---
seo-title: 암호 스크램블러
title: 암호 스크램블러
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# 암호 스크램블러 {#password-scrambler}

Password Scrambler 유틸리티는 암호를 암호화하여 Adobe Access Server for Protected Streaming 구성 파일에서 사용할 수 있도록 합니다. scrambler를 실행하려면 명령을 실행합니다.

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
>보호 스트리밍을 위한 Adobe Access Server의 암호 스크램블러 유틸리티는 참조 구현 라이센스 서버와 함께 제공되는 스크램블러와 호환되지 않습니다.


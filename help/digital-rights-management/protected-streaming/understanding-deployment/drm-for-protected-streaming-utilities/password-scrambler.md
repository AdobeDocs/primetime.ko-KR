---
description: 암호 스크램블러 유틸리티는 보호된 스트리밍 구성 파일에 대한 Adobe Primetime DRM 서버 암호를 암호화합니다.
title: 암호 스크램블러
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 암호 스크램블러 {#password-scrambler}

암호 스크램블러 유틸리티는 보호된 스트리밍 구성 파일에 대한 Adobe Primetime DRM 서버 암호를 암호화합니다.

스크램블러를 실행하려면 다음을 입력합니다.

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

또는

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

유틸리티는 다음 메시지를 표시합니다.

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

에 지정한 모든 암호 [!DNL flashaccess-global.xml] 및 [!DNL flashaccess-tenant.xml] 파일을 암호화해야 합니다.

>[!NOTE]
>
>보호 스트리밍을 위한 Primetime DRM 서버의 암호 스크램블러 유틸리티는 참조 구현 라이센스 서버와 함께 제공되는 스크램블러와 상호 교환될 수 없습니다.

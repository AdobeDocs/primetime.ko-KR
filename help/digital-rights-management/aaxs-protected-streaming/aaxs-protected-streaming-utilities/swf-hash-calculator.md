---
title: SWF 해시 계산기
description: SWF 해시 계산기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# SWF 해시 계산기{#swf-hash-calculator}

SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산했습니다. hasser를 실행하려면 명령을 실행합니다.

```
Hasher.bat filename.swf
```

또는 명령:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

이 유틸리티는 다음 메시지를 출력합니다.

```
SWF Hash: hash-of-swf
```

이 값은 [!DNL flashaccess-tenant.xml]에서 SWF 다이제스트를 지정하는 데 사용할 수 있습니다.

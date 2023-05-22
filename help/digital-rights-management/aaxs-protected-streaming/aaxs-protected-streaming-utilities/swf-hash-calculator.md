---
title: SWF 해시 계산기
description: SWF 해시 계산기
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# SWF 해시 계산기{#swf-hash-calculator}

SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산했습니다. 해셔를 실행하려면 다음 명령을 실행합니다.

```
Hasher.bat filename.swf
```

또는 명령:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

유틸리티가 다음 메시지를 출력합니다.

```
SWF Hash: hash-of-swf
```

이 값은 SWF 다이제스트를 지정하는 데 사용할 수 있습니다. [!DNL flashaccess-tenant.xml].

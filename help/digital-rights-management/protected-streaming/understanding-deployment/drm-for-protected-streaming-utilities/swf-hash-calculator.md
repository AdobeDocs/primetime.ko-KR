---
description: SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산합니다.
title: SWF 해시 계산기
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF 해시 계산기{#swf-hash-calculator}

SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산합니다.

해셔를 실행하려면 다음을 입력합니다.

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

또는

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

유틸리티는 다음 메시지를 표시합니다.

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

이 값을 사용하여에서 SWF 다이제스트를 지정할 수 있습니다. [!DNL flashaccess-tenant.xml].

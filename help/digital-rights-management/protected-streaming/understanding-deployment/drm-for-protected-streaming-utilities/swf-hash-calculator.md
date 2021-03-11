---
description: SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산합니다.
title: SWF 해시 계산기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# SWF 해시 계산기{#swf-hash-calculator}

SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산합니다.

hasser를 실행하려면 다음을 입력합니다.

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

or

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

이 유틸리티는 다음 메시지를 표시합니다.

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

이 값을 사용하여 [!DNL flashaccess-tenant.xml]에서 SWF 다이제스트를 지정할 수 있습니다.

---
description: SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산합니다.
seo-description: SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산합니다.
seo-title: SWF 해시 계산기
title: SWF 해시 계산기
uuid: 0cf972c1-4717-4d78-a594-b27178ece512
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# SWF 해시 계산기{#swf-hash-calculator}

SWF 해시 계산기 유틸리티는 파일에 있는 SWF 애플리케이션의 다이제스트를 계산합니다.

헤더를 실행하려면 다음을 입력합니다.

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

이 값을 사용하여 에서 SWF 다이제스트를 지정할 수 [!DNL flashaccess-tenant.xml]있습니다.

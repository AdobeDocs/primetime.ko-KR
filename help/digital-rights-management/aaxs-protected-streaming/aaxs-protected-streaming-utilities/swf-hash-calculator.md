---
seo-title: SWF 해시 계산기
title: SWF 해시 계산기
uuid: c1823208-92d9-47c5-b550-f9cc370b543d
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

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

이 값은 에서 SWF 다이제스트를 지정하는 데 사용할 수 [!DNL flashaccess-tenant.xml]있습니다.

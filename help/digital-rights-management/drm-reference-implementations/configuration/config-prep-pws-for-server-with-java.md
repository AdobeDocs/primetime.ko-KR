---
description: 'null'
seo-description: 'null'
seo-title: Java를 사용하여 암호 준비
title: Java를 사용하여 암호 준비
uuid: 8a708d22-764f-4229-95ca-109482563432
translation-type: tm+mt
source-git-commit: 055989cbe3a187516f18816492aaea709cc80c81
workflow-type: tm+mt
source-wordcount: '24'
ht-degree: 0%

---


# Java를 사용하여 암호 준비{#prepare-passwords-using-java}

Java로 `ScrambleUtil.class` 실행:

1. 탐색 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. 명령줄에서 다음을 입력합니다.

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```


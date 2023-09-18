---
title: Java를 사용하여 암호 준비
description: Java를 사용하여 암호 준비
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '22'
ht-degree: 0%

---

# Java를 사용하여 암호 준비{#prepare-passwords-using-java}

실행 `ScrambleUtil.class` Java 사용:

1. 다음으로 이동 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. 명령줄에서 다음을 입력합니다.

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

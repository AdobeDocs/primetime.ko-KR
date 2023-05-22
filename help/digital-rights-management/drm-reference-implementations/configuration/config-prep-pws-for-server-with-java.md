---
title: Java를 사용하여 암호 준비
description: Java를 사용하여 암호 준비
copied-description: true
exl-id: 69d551c4-e13b-473a-86ed-36b5ba24f6b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

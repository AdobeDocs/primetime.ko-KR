---
title: 문제 해결
description: 문제 해결
copied-description: true
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 문제 해결 {#troubleshooting}

다음은 배포에 대한 일반적인 문제 및 솔루션입니다.

* 다음 오류가 표시되면

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   제공된 을 사용하여 암호가 암호화되었는지 확인합니다. `ScrambleUtil` 클래스.

* 다음 오류가 표시되면

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   PFX 파일에 대해 올바른 암호화된 암호를 지정했는지 확인하십시오.

* 다음 오류가 표시되면

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   참조 구현과 함께 제공되는 암호 스크램블러 클래스를 사용했는지 확인합니다(이 스크램블러 유틸리티는 Adobe® Access™ Server for Protected Streaming과 함께 제공되는 것과 다름).

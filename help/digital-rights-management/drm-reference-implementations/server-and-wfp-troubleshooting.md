---
title: 문제 해결
description: 문제 해결
copied-description: true
exl-id: 6c4f15b6-507e-496e-ad1c-702ce77dd069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 문제 해결{#troubleshooting}

다음은 배포 중에 발생할 수 있는 몇 가지 문제와 해결 방법입니다.

* 다음 오류 메시지가 표시되는 경우:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   암호가 `ScrambleUtil` 클래스.

* 다음 오류 메시지가 표시되는 경우:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   PFX 파일에 올바른 암호화된 암호를 지정했는지 확인하십시오.

* 다음 오류 메시지가 표시되는 경우:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   암호 스크램블러 클래스를 사용하는지 확인합니다. *참조 구현과 함께 제공됩니다*. 이 스크램블러 유틸리티는 Protected Streaming용 Adobe Primetime DRM Server와 함께 제공된 것과는 다릅니다.

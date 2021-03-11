---
title: 문제 해결
description: 문제 해결
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# {#troubleshooting} 문제 해결

다음은 일반적인 배포 문제 및 해결책입니다.

* 다음 오류가 표시되는 경우:

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   제공된 `ScrambleUtil` 클래스를 사용하여 암호가 암호화되었는지 확인합니다.

* 다음 오류가 표시되는 경우:

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   PFX 파일에 대해 올바른 암호화된 암호를 지정했는지 확인하십시오.

* 다음 오류가 표시되는 경우:

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Reference Implementation과 함께 제공된 암호 scrambler 클래스를 사용했는지 확인하십시오. 이 scrambler 유틸리티는 보호 스트리밍을 위한 Adobe® Access™ Server와 함께 제공된 것과 다릅니다.


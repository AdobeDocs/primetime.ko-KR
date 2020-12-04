---
description: 'null'
seo-description: 'null'
seo-title: 문제 해결
title: 문제 해결
uuid: 06b86067-1ff6-4b4e-922f-7f968260ba19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 문제 해결{#troubleshooting}

배포 중에 발생할 수 있는 몇 가지 문제 및 해결 방법은 다음과 같습니다.

* 다음 오류 메시지가 표시되는 경우:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   암호가 `ScrambleUtil` 클래스로 암호화되었는지 확인합니다.

* 다음 오류 메시지가 표시되는 경우:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   PFX 파일에 올바른 암호화된 암호를 지정했는지 확인하십시오.

* 다음 오류 메시지가 표시되는 경우:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   참조 구현&#x200B;*과 함께 제공된 암호 scrambler 클래스*&#x200B;를 사용해야 합니다. 이 scrambler 유틸리티는 보호 스트리밍을 위해 Adobe Primetime DRM 서버와 함께 제공된 것과 다릅니다.


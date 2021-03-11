---
title: Ant를 사용하여 암호 준비
description: Ant를 사용하여 암호 준비
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---


# Ant{#prepare-passwords-using-ant}을(를) 사용하여 암호 준비

Ant를 사용하여 암호를 암호화합니다.

1. `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`으로 이동합니다.
1. Primetime DRM Java SDK가 포함된 디렉토리를 가리키도록 [!DNL build-refimpl.xml]의 `sdkdir` 속성을 설정합니다.
1. 다음 명령을 실행합니다.

   ```
   ant -f build-refimpl.xml
   ```


---
description: 'null'
seo-description: 'null'
seo-title: Ant를 사용하여 암호 준비
title: Ant를 사용하여 암호 준비
uuid: 9419ab0d-b448-4881-9d26-35c00f0b13bc
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '42'
ht-degree: 0%

---


# Ant{#prepare-passwords-using-ant}을(를) 사용하여 암호 준비

Ant를 사용하여 암호를 암호화합니다.

1. `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`으로 이동합니다.
1. Primetime DRM Java SDK가 포함된 디렉토리를 가리키도록 [!DNL build-refimpl.xml]에 `sdkdir` 속성을 설정합니다.
1. 다음 명령을 실행합니다.

   ```
   ant -f build-refimpl.xml
   ```


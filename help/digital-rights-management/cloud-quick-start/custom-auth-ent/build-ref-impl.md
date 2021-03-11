---
title: BEES 참조 구현 구축
description: BEES 참조 구현 구축
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# BEES 참조 구현 {#build-the-bees-reference-implementation} 구축

Java 1.6.0_24 이상을 사용하고 있는지 확인합니다.
1. [!DNL build-bees.xml]의 `tomcatdir` 및 `fasterxmldir`과 같이 필요한 빈 경로를 채웁니다.

   FasterXML/Jackson이 포함되어 있습니다. [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core)에서도 다운로드할 수 있습니다.
1. 다른 버전의 Jackson 라이브러리를 사용하려면 [!DNL build.common.xml]에서 실제 jar 파일 이름을 업데이트합니다.
1. [!DNL build-bees.xml]의 `all` 타겟을 실행합니다.

   ```
   ant -f build-bees.xml
   ```

[!DNL bees.war]은 [!DNL bees-build/wars] 폴더에 생성됩니다.
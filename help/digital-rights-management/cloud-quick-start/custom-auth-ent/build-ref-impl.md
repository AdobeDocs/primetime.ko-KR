---
seo-title: BEES 참조 구현 구축
title: BEES 참조 구현 구축
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# BEES 참조 구현 {#build-the-bees-reference-implementation} 빌드

Java 1.6.0_24 이상을 사용하고 있는지 확인합니다.
1. [!DNL build-bees.xml]의 `tomcatdir` 및 `fasterxmldir`과 같은 필요한 빈 경로를 채웁니다.

   FasterXML/Jackson 포함 [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core)에서도 다운로드할 수 있습니다.
1. 다른 버전의 Jackson 라이브러리를 사용하려면 [!DNL build.common.xml]에서 실제 jar 파일 이름을 업데이트하십시오.
1. [!DNL build-bees.xml]의 `all` 타겟을 실행합니다.

   ```
   ant -f build-bees.xml
   ```

[!DNL bees.war]은 [!DNL bees-build/wars] 폴더에 생성됩니다.
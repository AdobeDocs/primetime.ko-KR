---
seo-title: BEES 참조 구현 구축
title: BEES 참조 구현 구축
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# BEES 참조 구현 구축 {#build-the-bees-reference-implementation}

Java 1.6.0_24 이상을 사용하고 있는지 확인합니다.
1. 와 같은 필요한 빈 `tomcatdir` 경로를 `fasterxmldir` 채웁니다. [!DNL build-bees.xml]

   FasterXML/Jackson이 포함되어 있습니다. https://jar-download.com/artifacts/com.fasterxml.jackson.core에서 다운로드할 수도 [있습니다](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. 다른 버전의 Jackson 라이브러리를 사용하려는 [!DNL build.common.xml] 경우 실제 jar 파일 이름을 업데이트합니다.
1. 다음 `all` 대상을 실행합니다 [!DNL build-bees.xml].

   ```
   ant -f build-bees.xml
   ```

폴더가 [!DNL bees.war] 만들어집니다 [!DNL bees-build/wars] .
---
title: BEES 참조 구현 구축
description: BEES 참조 구현 구축
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# BEES 참조 구현 구축 {#build-the-bees-reference-implementation}

Java 1.6.0_24 이상을 사용 중인지 확인하십시오.
1. 다음과 같이 필요한 빈 경로를 입력합니다. `tomcatdir` 및 `fasterxmldir` 위치: [!DNL build-bees.xml]

   FasterXML/Jackson이 포함되어 있습니다. 에서 다운로드할 수도 있습니다. [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. 에서 실제 jar 파일 이름 업데이트 [!DNL build.common.xml] 다른 버전의 Jackson 라이브러리를 사용하려는 경우.
1. 실행 `all` 대상 [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

다음 [!DNL bees.war] 다음에서 생성됩니다. [!DNL bees-build/wars] 폴더를 삭제합니다.

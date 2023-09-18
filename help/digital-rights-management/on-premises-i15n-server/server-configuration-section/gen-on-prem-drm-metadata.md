---
title: 온-프레미스 DRM 메타데이터 생성
description: 온-프레미스 DRM 메타데이터 생성
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 온-프레미스 DRM 메타데이터 생성{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] 유틸리티는에 포함되어 있습니다. [!DNL create_metadata] 폴더를 삭제합니다. 이 유틸리티의 핵심은 클라이언트가 지정된 온-프레미스 개별화 서버에 대한 개별화 프로세스를 수행하도록 시작하는 온-프레미스 DRM 메타데이터를 만드는 것입니다.

1. Primetime DRM 참조 구현 - 명령줄 도구를 다음 파일로 업데이트합니다.

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

     두 JAR 파일이 [!DNL Command Line Tools/libs] 폴더를 삭제합니다. 다음 [!DNL createMetadata.properties] 파일은 다음 옆에 있을 수 있습니다. [!DNL flashaccesstools.properties] 파일.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

포함된 항목: [!DNL examplecreate.sh] 메타데이터의 샘플 생성을 보여 주는 스크립트. 메타데이터 생성을 시도하기 전에 스크립트 및 속성 파일 모두에서 라이선스 서버 URL 및 개인화 서버 URL을 구성해야 합니다.

유틸리티에 대한 입력은 다음과 같습니다.

* `createMetadata.properties` - 기본 정책, 인증서 위치 및 암호 등이 포함된 속성 파일
* `indivCert` - 개별화 전송 인증서가 포함된 PKCS12 파일
* `indivURL` - 온-프레미스 개별화 서버 URL

출력 파일은 DRM 클라이언트에서 사용할 온프레미스 DRM 메타데이터 파일입니다. 예:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.

---
seo-title: 온-프레미스 DRM 메타데이터 생성
title: 온-프레미스 DRM 메타데이터 생성
uuid: 89d53924-1a8d-42d4-a716-ce4f4566b6bf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 온-프레미스 DRM 메타데이터 생성{#generate-the-on-premises-drm-metadata}

[!DNL CreateMetadata.jar] 유틸리티는 [!DNL create_metadata] 폴더에 포함되어 있습니다. 이 유틸리티의 핵심은 온-프레미스 DRM 메타데이터를 만들어 클라이언트가 지정된 온-프레미스 개인화 서버에 대해 개인화 프로세스를 수행하도록 하는 것입니다.

1. Primetime DRM 참조 구현 - 명령줄 도구를 다음 파일로 업데이트합니다.

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      두 JAR 파일은 [!DNL Command Line Tools/libs] 폴더에 저장할 수 있습니다. [!DNL createMetadata.properties] 파일은 [!DNL flashaccesstools.properties] 파일 옆에 있을 수 있습니다.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

메타데이터의 샘플 생성을 설명하는 [!DNL examplecreate.sh] 스크립트가 포함되어 있습니다. 메타데이터 생성을 시도하기 전에 스크립트 및 속성 파일 모두에서 라이센스 서버 URL과 식별 서버 URL을 구성해야 합니다.

유틸리티에 대한 입력은 다음과 같습니다.

* `createMetadata.properties` - 기본 정책, 인증서 위치 및 암호 등을 포함하는 속성 파일
* `indivCert` - 개인화 전송 인증서를 포함하는 PKCS12 파일
* `indivURL` - 온-프레미스 개인화 서버의 URL

출력 파일은 DRM 클라이언트가 사용하는 온-프레미스 DRM 메타데이터 파일입니다. 예:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
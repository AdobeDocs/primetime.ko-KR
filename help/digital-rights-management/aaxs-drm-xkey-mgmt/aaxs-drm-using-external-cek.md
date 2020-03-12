---
description: 외부 CK 기능을 사용하여 기존 CKMS를 사용하여 라이선스를 확인하고 패키지화할 수 있습니다.
seo-description: 외부 CK 기능을 사용하여 기존 CKMS를 사용하여 라이선스를 확인하고 패키지화할 수 있습니다.
seo-title: 외부 CEK를 사용하여 라이선스 종료 및 패키지
title: 외부 CEK를 사용하여 라이선스 종료 및 패키지
uuid: 1bfd8c6c-4ae9-47de-8247-085b5360127d
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0

---


# 외부 CEK를 사용하여 라이선스 종료 및 패키지{#using-external-cek-to-vend-and-package-licenses}

외부 CK 기능을 사용하여 기존 CKMS를 사용하여 라이선스를 확인하고 패키지화할 수 있습니다.

## Encrypt 파섹

AAXS가 비디오를 암호화하고 CEK를 *포함하지 않는* 메타데이터를 만드는 명령줄 도구입니다(AAXS 라이선스 서버의 공개 인증서로 보호). 대신 이 도구는 CEK ID를 비디오의 메타데이터에 포함합니다.

라이센스 취득 동안 AAXS 라이센스 서버는 이 컨텐츠가 외부 CEK를 사용하여 보호되었다는 것을 식별하는 메타데이터에서 플래그를 관찰합니다. 라이센스 서버는 메타데이터에서 CEK ID를 추출한 다음 보안 저장소/CKMS를 쿼리하여 해당 CEK를 검색합니다.

## 패키징 워크플로우

1. Java 1.6.0_24 이상을 사용하고 있는지 확인합니다.
1. 도구 사용을 보려면: `java -jar AdobePackager_ExternalCEK.jar`
1. 컨텐츠를 패키지하려면 다음을 수행합니다.

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* 포함된 ANT를 사용하여 Java 소스 코드를 작성할 수 있습니다 `build-samples.xml`
>* Flash Access SDK( `adobe-flashaccess-sdk.jar`)는 클래스 경로에 있어야 합니다.
>



## 서버 워크플로우

1. 참조 구현을 설정합니다.
1. 존재하는 경우 이전 참조 구현 배포를 정리합니다.

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. 다음 [!DNL CEKDepot.properties] 파일 옆에 [!DNL flashaccess-refimpl.properties]

1. Adobe Primetime 플레이어에서 라이선스 요청 시작
1. 다음과 유사한 사항을 위해 참조 임팔 로그를 관찰합니다.

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. 설정을 변경하여 [!DNL log4j.xml] 수준에서( `DEBUG` `INFO` 기본적으로 설정됨) 로그인해야 할 수 있습니다.

## 알려진 문제

없음

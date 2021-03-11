---
description: 기존 CKMS를 사용하여 라이선스를 확인하고 패키징하려면 외부 CEK 기능을 사용하십시오.
title: 외부 CEK를 사용하여 라이선스 구매 및 패키지
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# 외부 CEK를 사용하여 라이센스 종료 및 패키지{#using-external-cek-to-vend-and-package-licenses}

기존 CKMS를 사용하여 라이선스를 확인하고 패키징하려면 외부 CEK 기능을 사용하십시오.

## EncryptContentWithExternalKey.java

이 도구는 AAXS가 비디오를 암호화하고 *이(가) CEK(*&#x200B;에 AAXS 라이센스 서버의 공개 인증서로 보호됨)를 포함하지 않는 메타데이터를 만드는 명령줄 도구입니다. 대신 이 도구는 비디오의 메타데이터에 CEK ID를 포함합니다.

라이센스 취득 동안 AAXS 라이센스 서버는 이 컨텐츠가 외부 CEK를 사용하여 보호되었다는 것을 식별하는 메타데이터를 통해 플래그를 확인합니다. 라이센스 서버는 메타데이터에서 CEK ID를 추출하고 보안 저장소/CKMS를 쿼리하여 적절한 CEK를 검색합니다.

## 패키징 워크플로우

1. Java 1.6.0_24 이상을 사용하고 있는지 확인합니다.
1. 도구 사용을 보려면:`java -jar AdobePackager_ExternalCEK.jar`
1. 컨텐츠를 패키지화하려면:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Java 소스 코드는 포함된 ANT `build-samples.xml`를 사용하여 작성할 수 있습니다.
>* Flash Access SDK( `adobe-flashaccess-sdk.jar`)는 클래스 경로에 있어야 합니다.

>



## 서버 워크플로

1. 참조 구현을 설정합니다.
1. 존재하는 경우 이전 참조 구현 배포를 정리합니다.

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. [!DNL flashaccess-refimpl.properties] 옆에 [!DNL CEKDepot.properties] 파일이 있는지 확인합니다.

1. Adobe Primetime Player에서 라이선스 요청 시작
1. 다음과 유사한 작업을 위해 참조 구현 로그를 관찰합니다.

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. `DEBUG` 수준으로 기록하려면 [!DNL log4j.xml] 설정을 변경해야 할 수 있습니다( `INFO`는 기본적으로 설정되어 있음).

## 알려진 문제

없음

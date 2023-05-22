---
description: 외부 CEK 기능을 사용하여 기존 CKMS를 사용하여 라이센스를 검증하고 패키징합니다.
title: 외부 CEK를 사용하여 라이선스 갱신 및 패키지
exl-id: 3944624a-099e-4fc0-b829-6ab154a53758
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 외부 CEK를 사용하여 라이선스 갱신 및 패키지{#using-external-cek-to-vend-and-package-licenses}

외부 CEK 기능을 사용하여 기존 CKMS를 사용하여 라이센스를 검증하고 패키징합니다.

## EncryptContentWithExternalKey.java

이는 AAXS가 비디오를 암호화하고 *아님* 에는 CEK(AAXS 라이선스 서버의 공개 인증서로 보호됨)가 포함되어 있습니다. 대신 이 도구는 CEK ID를 비디오의 메타데이터에 임베드합니다.

라이센스 획득 중에 AAXS 라이센스 서버는 메타데이터에서 이 콘텐츠가 외부 CEK를 사용하여 보호되었음을 식별하는 플래그를 확인합니다. 라이센스 서버는 메타데이터에서 CEK ID를 추출한 다음 보안 저장소/CKMS를 쿼리하여 적절한 CEK를 검색합니다.

## 패키징 워크플로

1. Java 1.6.0_24 이상을 사용 중인지 확인하십시오.
1. 도구 사용을 보려면 다음을 수행하십시오. `java -jar AdobePackager_ExternalCEK.jar`
1. 콘텐츠를 패키지하려면 다음을 수행하십시오.

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Java 소스 코드는 포함된 ANT를 사용하여 빌드할 수 있습니다 `build-samples.xml`
>* Flash Access SDK( `adobe-flashaccess-sdk.jar`)는 클래스 경로에 있어야 합니다.
>


## 서버 워크플로우

1. 참조 구현을 설정합니다.
1. 존재하는 경우 이전 참조 구현 배포를 정리합니다.

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. 다음 항목이 있는지 확인합니다. [!DNL CEKDepot.properties] 와 함께 파일 [!DNL flashaccess-refimpl.properties]

1. Adobe Primetime 플레이어에서 라이선스 요청 시작
1. Ref Impl 로그에서 다음과 유사한 내용을 관찰하십시오.

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. 을(를) 변경해야 할 수 있습니다. [!DNL log4j.xml] 에 기록할 설정 `DEBUG` 수준 ( `INFO` 기본적으로 설정됨)

## 알려진 문제

없음

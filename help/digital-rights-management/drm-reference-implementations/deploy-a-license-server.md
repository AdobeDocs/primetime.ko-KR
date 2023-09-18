---
title: 라이선스 서버 배포
description: 라이선스 서버 배포
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 라이선스 서버 배포{#deploy-the-license-server}

1. 참조 구현 war 파일을 `webapps` Tomcat 서버의 디렉토리입니다.

   참조 구현 라이선스 서버를 그대로 사용하려면 라이선스 서버 WAR 파일( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) 로 이동합니다. `webapps` Tomcat 서버의 디렉토리입니다.

   참조 구현 라이선스 서버를 사용자 정의하는 경우 빌드한 서버 war 파일을 복사합니다. `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` (으)로 `webapps` 디렉토리.

   >[!NOTE]
   >
   >이전에 라이센스 서버 WAR 파일을 배포한 경우 [!DNL webapps] tomcat 서버의 디렉토리:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]

   >[!NOTE]
   >
   >배포 안 함 [!DNL edsws.war] Flash 미디어 Rights Management(FMRMS) v1.5 콘텐츠와의 이전 버전과의 호환성이 필요하지 않은 경우. (이는 매우 드문 요구 사항입니다.)
   >
   >Tomcat이 WAR 파일의 압축을 푸는 것을 방지하려면 다음을 편집합니다. `server.xml` 다음에서 `conf` 디렉터리 및 설정 `unpackWARs` 끝 `false`.

1. 의 전체 컨텐츠를 복사합니다. `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` 디렉토리 입력 [!DNL tomcat] 디렉토리.

   다음 [!DNL resources] 디렉터리에는 다음이 포함됩니다.

   * [!DNL flashaccesstools.properties] - 라이센스 서버 속성 파일입니다.
   * [!DNL log4j.xml] - 라이선스 서버 로깅 구성
   * [!DNL *.pol] - 샘플 DRM 정책 파일.

   또한 Adobe 인증 파일을 이 위치에 복사하도록 선택할 수도 있습니다.

1. 에서 라이선스 서버 설정 수정 [!DNL flashaccesstools.properties] 서버 설정을 반영합니다.

   최소한 다음 속성에 대한 값을 설정하십시오.

   * `config.resourcesDirectory`
   * `HandlerConfiguration.ServerTransportCredential`
   * `HandlerConfiguration.ServerTransportCredential.password`
   * `LicenseHandler.ServerCredential`
   * `LicenseHandler.ServerCredential.password`
   * `MetaDataConverter.SignatureParameters.ServerCredential`
   * `MetaDataConverter.SignatureParameters.ServerCredential.password`
   * `V2KeyParameters.LicenseServerUrl`
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate`
   * V2KeyParameters.LicenseServerTransportCertificate

1. 편집 `catalina.properties` Tomcat의 파일 `conf` 디렉터리, 위치 추가 [!DNL resources] 디렉토리(또는 등록 정보 파일 및 기타 리소스 파일을 저장한 대체 위치)를에 `shared.loader` 속성.

   예를 들어 `flashaccess-refimpl.properties` [!DNL]에 위치 [Tomcat 홈]\resources\]:

   ```
   shared.loader=..\resources
   ```

   이 위치 `flashaccess-refimpl.properties` 클래스 경로에 있습니다.
1. 다른 리소스 파일( [!DNL log4j.xml], 정책 파일, 인증)은 [!DNL resources] 디렉토리나 그렇지 않으면 클래스 경로와 위치에 지정된 [!DNL flashaccess-refimpl.properties].

   처음에는 을(를) 실행하려고 합니다. `log4j` 디버그 모드입니다. 위치 [!DNL log4j.xml], 설정됨 `debug` true로 변환:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Tomcat에서 [!DNL bin] 디렉토리, 서버를 시작합니다.

   Linux의 경우:

   ```
   catalina.sh start
   ```

   Windows:

   ```
   catalina.bat start
   ```

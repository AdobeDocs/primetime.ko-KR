---
description: 'null'
seo-description: 'null'
seo-title: 라이선스 서버 배포
title: 라이선스 서버 배포
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 29149594c4b41956a091ef27093304e74ff15f2f

---


# 라이선스 서버 배포{#deploy-the-license-server}

1. 참조 구현 전쟁 파일을 Tomcat 서버의 `webapps` 디렉토리에 복사합니다.

   참조 구현 라이센스 서버를 그대로 사용하려면 라이센스 서버 WAR 파일( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)을 Tomcat 서버의 `webapps` 디렉토리로 복사하면 됩니다.

   참조 구현 라이센스 서버를 사용자 지정하는 경우 작성한 서버 전쟁 파일을 `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` `webapps` 디렉토리로 복사합니다.

   >[!NOTE]
   >
   >이전에 라이센스 서버 WAR 파일을 배포한 경우 Tomcat 서버의 [!DNL webapps] 디렉토리에서 압축을 푼 WAR 디렉토리를 삭제해야 할 수 있습니다.       >
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >FMRMS(Flash Media Rights Management) v1.5 컨텐츠와의 이전 버전과의 호환성이 [!DNL edsws.war] 필요하지 않은 경우 배포하지 마십시오. (이는 매우 드문 요구 사항입니다.)
   >
   >Tomcat이 WAR 파일의 압축을 풀지 않도록 하려면 `server.xml` 디렉토리에서 `conf` 편집한 후 `unpackWARs` 로 설정합니다 `false`.

1. 디렉토리의 전체 컨텐츠를 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` [!DNL tomcat] 디렉토리에 복사합니다.

   이 [!DNL resources] 디렉토리에는 다음이 포함됩니다.

   * [!DNL flashaccesstools.properties] - 라이센스 서버 속성 파일입니다.
   * [!DNL log4j.xml] - 라이센스 서버 로깅 구성
   * [!DNL *.pol] - 샘플 DRM 정책 파일
   또한 Adobe 인증 파일을 이 위치에 복사할 수도 있습니다.

1. 서버 설정을 [!DNL flashaccesstools.properties] 반영하도록 라이센스 서버 설정을 수정합니다.

   최소한 다음 속성에 대한 값을 설정합니다.

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

1. Tomcat `catalina.properties` 디렉토리에서 `conf` 파일을 편집합니다.속성 파일과 기타 리소스 파일을 저장한 [!DNL resources] 디렉토리 또는 대체 위치를 속성에 추가합니다 `shared.loader` .

   예를 들어 [!DNL Tomcat home `flashaccess-refimpl.properties` \resources\ []]에 있는 경우:

   ```
   shared.loader=..\resources
   ```

   이것은 `flashaccess-refimpl.properties` 클래스 경로에 있습니다.
1. 다른 리소스 파일( [!DNL log4j.xml]정책 파일, 인증)이 [!DNL resources] 디렉토리에 있거나 클래스 경로 및 에 지정된 위치에 있는지 확인합니다 [!DNL flashaccess-refimpl.properties].

   처음에는 디버그 `log4j` 모드에서 실행되어야 합니다. 에서 [!DNL log4j.xml]true로 `debug` 설정합니다.

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Tomcat [!DNL bin] 디렉토리에서 서버를 시작합니다.

   Linux의 경우:

   ```
   catalina.sh start
   ```

   Windows:

   ```
   catalina.bat start
   ```

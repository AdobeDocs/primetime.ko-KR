---
title: 라이선스 서버 배포
description: 라이선스 서버 배포
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 라이선스 서버 {#deploy-the-license-server} 배포

1. 참조 구현 전쟁 파일을 Tomcat 서버의 `webapps` 디렉토리로 복사합니다.

   참조 구현 라이선스 서버를 그대로 사용하려면 라이센스 서버 WAR 파일( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)을 Tomcat 서버의 `webapps` 디렉토리로 간단히 복사할 수 있습니다.

   참조 구현 라이센스 서버를 사용자 정의하는 경우 `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars`에서 작성한 서버 전쟁 파일을 `webapps` 디렉토리로 복사합니다.

   >[!NOTE]
   >
   >이전에 라이센스 서버 WAR 파일을 배포한 경우 Tomcat 서버의 [!DNL webapps] 디렉토리에 있는 압축 해제된 WAR 디렉토리를 삭제해야 할 수 있습니다.
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >FMRMS(Flash 미디어 Rights Management) v1.5 컨텐츠와의 이전 버전과의 호환성이 필요하지 않은 경우 [!DNL edsws.war]을(를) 배포하지 마십시오. (이는 매우 드문 요구 사항입니다.)
   >
   >Tomcat이 WAR 파일의 압축을 해제하지 않도록 하려면 `conf` 디렉토리에서 `server.xml`을(를) 편집하고 `unpackWARs`를 `false`로 설정합니다.

1. `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` 디렉토리의 전체 내용을 [!DNL tomcat] 디렉토리로 복사합니다.

   [!DNL resources] 디렉토리에는 다음이 포함됩니다.

   * [!DNL flashaccesstools.properties] - 라이센스 서버 속성 파일입니다.
   * [!DNL log4j.xml] - 라이센스 서버 로깅 구성
   * [!DNL *.pol] - 샘플 DRM 정책 파일.

   또한 Adobe 인증 파일을 이 위치에 복사하도록 선택할 수도 있습니다.

1. 서버 설정을 반영하도록 [!DNL flashaccesstools.properties]의 라이센스 서버 설정을 수정합니다.

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

1. Tomcat `conf` 디렉토리에서 `catalina.properties` 파일을 편집합니다.[!DNL resources] 디렉터리 위치(또는 속성 파일 및 기타 리소스 파일을 저장한 대체 위치)를 `shared.loader` 속성에 추가합니다.

   예를 들어 [!DNL [Tomcat home]\resources\]에 `flashaccess-refimpl.properties`이(가) 있는 경우:

   ```
   shared.loader=..\resources
   ```

   그러면 클래스 경로에 `flashaccess-refimpl.properties`이(가) 배치됩니다.
1. 다른 리소스 파일( [!DNL log4j.xml], 정책 파일, 인증)이 [!DNL resources] 디렉토리에 있거나 다른 경우에는 [!DNL flashaccess-refimpl.properties]에 지정된 클래스 경로 및 해당 위치에 있는지 확인합니다.

   디버그 모드에서 처음에는 `log4j`을(를) 실행할 가능성이 있습니다. [!DNL log4j.xml]에서 `debug`을 true로 설정합니다.

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Tomcat [!DNL bin] 디렉토리에서 서버를 시작합니다.

   Linux의 경우:

   ```
   catalina.sh start
   ```

   Windows의 경우:

   ```
   catalina.bat start
   ```

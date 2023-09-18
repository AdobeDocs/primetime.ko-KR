---
title: Primetime DRM 키 서버 배포 개요
description: Primetime DRM 키 서버 배포 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# Primetime DRM 키 서버 배포 {#deploy-the-primetime-drm-key-server}

Primetime DRM 키 서버를 배포하기 전에 필요한 Java 및 Tomcat 버전을 설치했는지 확인하십시오. 다음을 참조하십시오. [DRM 키 서버 요구 사항](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Primetime DRM 키 서버 다운로드에는 다음이 포함됩니다 [!DNL faxsks.war]. 이 WAR 파일을 배포하려면 파일을 Tomcat [!DNL webapps] 디렉토리. 이전에 WAR 파일을 배포한 경우 압축을 푼 WAR 디렉토리를 수동으로 삭제해야 할 수 있습니다. [!DNL faxsks] 톰캣 [!DNL webapps] directory). Tomcat이 WAR 파일의 압축을 푸는 것을 방지하려면 [!DNL server.xml] Tomcat의 파일 [!DNL conf] 디렉터리 및 설정 `unpackWARs` 특성 대상 `false`.

Primetime DRM 키 서버는 선택적으로 플랫폼별 라이브러리(`jsafe.dll` Windows 또는 `libjsafe.so` Linux의 경우) 을 참조하십시오. 다음에서 플랫폼에 적절한 라이브러리를 복사합니다. `thirdparty/cryptoj/platform` 에 의해 지정된 위치로 `PATH` 환경 변수(또는 `LD_LIBRARY_PATH` Linux에서).

>[!NOTE]
>
>의 64비트 버전 [!DNL jsafe] 운영 체제와 JDK가 모두 64비트를 지원하는 경우에만 라이브러리를 사용하고 그렇지 않으면 32비트 버전을 사용해야 합니다.

## SSL 구성 {#ssl-configuration}

원격 HTTPS 키 전달에는 SSL이 필요합니다. SSL 연결은 애플리케이션 서버(즉, Tomcat에서 SSL을 구성함)에서 처리하거나 다른 서버(예: 로드 밸런서, SSL 가속기 또는 Apache)에서 처리할 수 있습니다. 원격 HTTPS 키 전달에는 SSL 연결이 필요합니다. 서버에는 신뢰할 수 있는 CA에서 발급한 SSL 인증서가 필요합니다.

SSL을 구성하는 옵션은 다양합니다. 다음은 Apache 및 Tomcat에서 클라이언트 인증을 사용하여 SSL을 구성하는 예입니다.

다음 예는 Apache SSL 구성을 보여줍니다.

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

다음 예는 Tomcat SSL 구성을 보여줍니다. 인증서 및 키 파일을 생성하려면 다음을 수행합니다.

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

공통 이름을 입력하라는 메시지가 표시되면 서버의 FQDN(정규화된 도메인 이름)을 사용하십시오.

복사 [!DNL server.cer], 및 [!DNL server.key] Tomcat 디렉토리로 이동합니다. 에서 다음 커넥터를 지정합니다 [!DNL conf/server.xml]:

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Java 시스템 속성 {#java-system-properties}

Primetime DRM 키 서버에 대한 구성 및 로그 파일의 위치를 수정하기 위해 다음 두 Java 시스템 속성을 설정하는 옵션이 있습니다.

* `KeyServer.ConfigRoot` - 이 디렉토리에는 Primetime DRM 키 서버에 대한 모든 구성 파일이 포함되어 있습니다. 이러한 파일의 내용에 대한 자세한 내용은 [키 서버 구성 파일](#key-server-configuration-files). 설정하지 않으면 기본값은 입니다. [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - iOS 키 서버 응용 프로그램 로그가 포함된 로그 디렉터리입니다. 설정하지 않으면 기본값은 와 같습니다. `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Xbox Key Server 응용 프로그램 로그가 들어 있는 로그 디렉터리입니다. 설정하지 않으면 기본값이 와 같습니다. `KeyServer.ConfigRoot`.

을 사용하는 경우 [!DNL catalina.bat] 또는 [!DNL catalina.sh] tomcat을 시작하려면 다음을 사용하여 이러한 시스템 속성을 쉽게 설정할 수 있습니다. `JAVA_OPTS` 환경 변수입니다. Tomcat을 시작할 때 여기에 설정된 모든 Java 옵션이 사용됩니다. 예를 들어 다음을 설정합니다.

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM 자격 증명 {#primetime-drm-credentials}

Primetime DRM iOS 및 Xbox 360 클라이언트의 키 요청을 처리하려면 Adobe에서 발급한 자격 증명 집합으로 Primetime DRM 키 서버를 구성해야 합니다. 이러한 자격 증명은 PKCS#12에 저장할 수 있습니다( [!DNL .pfx]) 파일 또는 HSM에 있습니다.

다음 [!DNL .pfx] 파일을 어디든 찾을 수 있지만, 쉽게 구성할 수 있도록 Adobe에서는 [!DNL .pfx] 테넌트의 구성 디렉터리에 있는 파일입니다. 자세한 내용은 [키 서버 구성 파일](#key-server-configuration-files).

### HSM 구성 {#section_13A19E3E32934C5FA00AEF621F369877}

HSM을 사용하여 서버 자격 증명을 저장하기로 선택한 경우 HSM에 개인 키와 인증서를 로드하고 *pkcs11.cfg* 구성 파일입니다. 이 파일은 다음 위치에 있어야 합니다. *KeyServer.ConfigRoot* 디렉토리. 다음을 참조하십시오. `<Primetime DRM Key Server>/configs` 예제 PKCS 11 구성 파일의 디렉토리입니다. 형식에 대한 자세한 내용은 [!DNL pkcs11.cfg]Sun PKCS11 공급자 설명서를 참조하십시오.

HSM 및 Sun PKCS11 구성 파일이 제대로 구성되어 있는지 확인하려면 [!DNL pkcs11.cfg] 파일이 있습니다( [!DNL keytool] 는 Java JRE 및 JDK와 함께 설치됩니다).

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에 자격 증명이 표시되면 HSM이 제대로 구성되고 키 서버가 자격 증명에 액세스할 수 있습니다.

## 키 서버 구성 파일 {#key-server-configuration-files}

Primetime DRM 키 서버에는 두 가지 유형의 구성 파일이 필요합니다.

* 전역 구성 파일, [!DNL flashaccess-keyserver-global.xml]
* 각 테넌트에 대한 테넌트 구성 파일 [!DNL flashaccess-keyserver-tenant.xml]

구성 파일이 변경된 경우 변경 사항을 적용하려면 서버를 다시 시작해야 합니다.

구성 파일에서 암호를 일반 텍스트로 사용할 수 없도록 하려면 전역 및 테넌트 구성 파일에 지정된 모든 암호를 암호화해야 합니다. 암호의 암호화와 관련된 자세한 내용은 [*암호 스크램블러* 위치: *보호된 스트리밍에 Primetime DRM 서버 사용*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## 디렉터리 구조 구성 {#configuration-directory-structure}

구성 디렉토리의 구조는 다음과 같습니다.

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## 전역 구성 파일 {#global-configuration-file}

다음 [!DNL flashaccess-keyserver-global.xml] 구성 파일에는 키 서버의 모든 테넌트에 적용되는 설정이 포함되어 있습니다. 이 파일은 다음 위치에 있어야 합니다. `KeyServer.ConfigRoot`. 다음을 참조하십시오. [!DNL configs] 예제 전역 구성 파일에 대한 디렉토리입니다. 전역 구성 파일에는 다음 항목이 포함되어 있습니다.

* 로깅 - 로깅 수준 및 로그 파일이 롤링되는 빈도를 지정합니다.
* HSM 암호 - HSM이 서버 자격 증명을 저장하는 데 사용되는 경우에만 필요합니다.

에 있는 예제 전역 구성 파일의 주석을 참조하십시오 `<Primetime DRM Key Server>/configs` 을 참조하십시오.

## 테넌트 구성 파일 {#tenant-configuration-files}

다음 [!DNL flashaccess-ioskeyserver-tenant.xml] 및 [!DNL flashaccess-xboxkeyserver-tenant.xml] 구성 파일에는 Primetime DRM 키 서버의 특정 테넌트에 적용되는 설정이 포함되어 있습니다. 각 테넌트에는 이러한 구성 파일의 자체 인스턴스가 있습니다. [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. 다음을 참조하십시오. [!DNL configs/faxsks/tenants/sampletenant] 예제 테넌트 구성 파일의 디렉토리입니다.

테넌트 구성 파일의 모든 파일 경로를 절대 경로 또는 테넌트의 구성 디렉터리( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

모든 테넌트 구성 파일은 다음과 같습니다.

* 키 서버 자격 증명 - Adobe에서 발급한 하나 이상의 키 서버 자격 증명(인증서 및 개인 키)을 지정합니다. 에 대한 경로로 지정할 수 있습니다. [!DNL .pfx] 파일 및 암호 또는 HSM에 저장된 자격 증명의 별칭. 이러한 여러 자격 증명을 파일 경로나 키 별칭 또는 둘 다로 여기에 지정할 수 있습니다.

다음 **iOS** 테넌트 구성 파일에는 다음이 포함됩니다.

* 키 배달 창 - (선택 사항) 키 배달 요청 타임스탬프 유효성 기간(초)을 지정합니다. 기본값은 500초입니다.

다음 **Xbox 360** 테넌트 구성 파일에는 다음이 포함됩니다.

* XSTS 자격 증명 - XSTS 토큰을 해독하는 데 사용되는 응용 프로그램 개발자의 자격 증명을 지정합니다.
* XSTS 서명 인증서 - XSTS 토큰의 서명을 확인하는 데 사용되는 인증서를 지정합니다.
* Packager 허용 목록 - 키 서버에서 신뢰하는 Packager 인증서. 목록에 포함된 패키지 인증서가 없으면 모든 패키지 인증서를 신뢰할 수 있습니다.

## 로그 파일 {#log-files}

Primetime DRM 키 서버 응용 프로그램에서 생성된 로그 파일( [!DNL flashaccess-ioskeyserver_*.log] 및 [!DNL flashaccess-xboxkeyserver_*.log])은(는) 다음 사용자가 지정한 디렉터리에 있습니다. `KeyServer.LogRoot`.

로그 파일은 클라이언트 유형별로 구분됩니다. 클라이언트 유형당 두 개의 로그가 있습니다.

* An *액세스 로그* - 요청 및 응답만 모니터링
* A *컨텍스트 로그* - 자세한 오류 메시지 및 스택 추적이 포함되어 있습니다.

## 키 서버 시작 {#starting-the-key-server}

키 서버를 시작하려면 Tomcat을 시작합니다.

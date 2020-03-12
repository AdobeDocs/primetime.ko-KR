---
seo-title: Primetime DRM 키 서버 배포 개요
title: Primetime DRM 키 서버 배포 개요
uuid: 86630675-c15d-4f32-8212-d7343f4f92e0
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# Primetime DRM 키 서버 배포 {#deploy-the-primetime-drm-key-server}

Primetime DRM 키 서버를 배포하기 전에 필요한 버전의 Java 및 Tomcat을 설치했는지 확인하십시오. DRM [주요 서버 요구 사항을 참조하십시오](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Primetime DRM Key Server 다운로드에는 다음이 포함되어 [!DNL faxsks.war]있습니다. 이 WAR 파일을 배포하려면 파일을 Tomcat의 [!DNL webapps] 디렉토리에 복사합니다. 이전에 WAR 파일을 배포한 경우 Tomcat의 [!DNL faxsks] [!DNL webapps] 디렉토리에서 압축을 푼 WAR 디렉토리를 수동으로 삭제해야 할 수 있습니다. Tomcat이 WAR 파일의 압축을 풀지 않도록 하려면 Tomcat의 [!DNL server.xml] 디렉토리에서 [!DNL conf] 파일을 편집하고 `unpackWARs` 속성을 `false`로 설정합니다.

Primetime DRM 키 서버는 선택적으로 플랫폼 전용 라이브러리(Windows`jsafe.dll` 또는 Linux `libjsafe.so` 에서)를 사용하여 성능을 향상시켰습니다. 환경 변수(또는 Linux `thirdparty/cryptoj/platform` `PATH` `LD_LIBRARY_PATH` 에서)에 의해 지정된 위치에 플랫폼에 적합한 라이브러리를 복사합니다.

>[!NOTE]
>
>64비트 버전의 [!DNL jsafe] 라이브러리는 운영 체제와 JDK가 모두 64비트를 지원하는 경우에만 사용해야 하며, 그렇지 않은 경우 32비트 버전을 사용해야 합니다.

## SSL 구성 {#ssl-configuration}

원격 HTTPS 키 전달에는 SSL이 필요합니다. SSL 연결은 응용 프로그램 서버(즉, Tomcat에서 SSL을 구성하여 처리하거나, 다른 서버(즉, 로드 밸런서, SSL 가속기 또는 Apache)에서 처리할 수 있습니다. 원격 HTTPS 키를 배달하려면 SSL 연결이 필요합니다. 서버에 신뢰할 수 있는 CA에서 발급한 SSL 인증서가 필요합니다.

SSL을 구성하기 위한 다양한 옵션이 있습니다. 다음은 Apache 및 Tomcat에서 클라이언트 인증을 사용하여 SSL을 구성하는 예입니다.

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

일반 이름을 입력하라는 메시지가 표시되면 서버의 FQDN(정규화된 도메인 이름)을 사용합니다.

Tomcat [!DNL server.cer][!DNL server.key] 디렉토리로 복사합니다. 다음 커넥터를 [!DNL conf/server.xml]지정합니다.

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

다음 두 개의 Java 시스템 속성을 설정하여 Primetime DRM 키 서버에 대한 구성 및 로그 파일의 위치를 수정할 수 있습니다.

* `KeyServer.ConfigRoot` - 이 디렉토리에는 Primetime DRM 키 서버에 대한 모든 구성 파일이 포함되어 있습니다. 이러한 파일의 내용에 대한 자세한 내용은 주요 서버 [구성 파일을](#key-server-configuration-files)참조하십시오. 설정하지 않으면 기본값은 [!DNL CATALINA_BASE/keyserver]입니다.

* `KeyServer.LogRoot` - iOS 키 서버 응용 프로그램 로그가 포함된 로그 디렉토리입니다. 설정하지 않으면 기본값은 `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Xbox 키 서버 응용 프로그램 로그가 포함된 로그 디렉토리입니다. 설정하지 않으면 기본값은 `KeyServer.ConfigRoot`동일합니다.

Tomcat을 사용하거나 [!DNL catalina.bat] 시작하는 경우 [!DNL catalina.sh] `JAVA_OPTS` 환경 변수를 사용하여 이러한 시스템 속성을 쉽게 설정할 수 있습니다. 여기에 설정된 모든 Java 옵션은 Tomcat이 시작될 때 사용됩니다. 예를 들어 다음과 같이 설정합니다.

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM 자격 증명 {#primetime-drm-credentials}

Primetime DRM iOS 및 Xbox 360 클라이언트의 주요 요청을 처리하려면 Adobe에서 발행한 자격 증명 세트로 Primetime DRM 키 서버를 구성해야 합니다. 이러한 자격 증명은 PKCS#12 ( [!DNL .pfx]) 파일 또는 HSM에 저장할 수 있습니다.

파일은 [!DNL .pfx] 어디에서나 위치할 수 있지만 쉽게 구성하려면 테넌트의 구성 디렉토리에 [!DNL .pfx] 파일을 배치하는 것이 좋습니다. 자세한 내용은 주요 서버 [구성 파일을](#key-server-configuration-files)참조하십시오.

### HSM 구성 {#section_13A19E3E32934C5FA00AEF621F369877}

HSM을 사용하여 서버 자격 증명을 저장하도록 선택한 경우 개인 키 및 인증서를 HSM에 로드하고 *pkcs11.cfg* 구성 파일을 생성해야 합니다. 이 파일은 KeyServer.ConfigRoot *디렉토리에 있어야* 합니다. 자세한 내용은 [!DNL <Primetime DRM Key Server>/configs] 디렉토리를 참조하십시오. 형식(형식)에 대한 자세한 [!DNL pkcs11.cfg]내용은 Sun PKCS11 공급자 설명서를 참조하십시오.

HSM 및 Sun PKCS11 구성 파일이 제대로 구성되어 있는지 확인하려면 [!DNL pkcs11.cfg] 파일이 있는 디렉토리에서 다음 명령을 사용합니다(Java JRE 및 JDK와 함께 [!DNL keytool] 설치).

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

목록에 자격 증명이 표시되면 HSM이 제대로 구성되고 키 서버가 자격 증명을 액세스할 수 있습니다.

## 주요 서버 구성 파일 {#key-server-configuration-files}

Primetime DRM 키 서버에는 두 가지 유형의 구성 파일이 필요합니다.

* 전역 구성 파일, [!DNL flashaccess-keyserver-global.xml]
* 각 테넌트에 대한 테넌트 구성 파일, [!DNL flashaccess-keyserver-tenant.xml]

구성 파일을 변경하면 변경 사항을 적용하려면 서버를 다시 시작해야 합니다.

구성 파일의 투명한 텍스트로 암호를 사용하지 않으려면 전역 및 테넌트 구성 파일에 지정된 모든 암호를 암호화해야 합니다. 암호 암호화에 대한 자세한 내용은 보호된 스트리밍을 [*위한 Primetime DRM *서버*&#x200B;사용의 암호 스크램블러를 참조하십시오&#x200B;*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## 구성 디렉토리 구조 {#configuration-directory-structure}

구성 디렉토리에는 다음과 같은 구조가 있습니다.

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

이 [!DNL flashaccess-keyserver-global.xml] 구성 파일에는 키 서버의 모든 테넌트에 적용되는 설정이 들어 있습니다. 이 파일은 에 있어야 합니다 `KeyServer.ConfigRoot`. 전역 구성 파일의 예는 [!DNL configs] 디렉토리를 참조하십시오. 전역 구성 파일에는 다음이 포함됩니다.

* 로깅 - 로깅 수준 및 로그 파일의 롤링 빈도를 지정합니다.
* HSM 암호 - 서버 자격 증명을 저장하는 데 HSM을 사용하는 경우에만 필요합니다.

See the comments in the example global configuration file located in [!DNL <Primetime DRM Key Server>/configs] for more details.

## 테넌트 구성 파일 {#tenant-configuration-files}

Primetime DRM 키 [!DNL flashaccess-ioskeyserver-tenant.xml] 서버의 특정 테넌트에 적용되는 및 [!DNL flashaccess-xboxkeyserver-tenant.xml] 구성 파일에는 설정이 들어 있습니다. 각 테넌트는 에 있는 이러한 구성 파일의 자체 인스턴스를 가지고 [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]있습니다. 테넌트 구성 파일의 예는 [!DNL configs/faxsks/tenants/sampletenant] 디렉토리를 참조하십시오.

테넌트 구성 파일의 모든 파일 경로를 테넌트의 구성 디렉토리( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname])에 상대적인 절대 경로 또는 경로로 지정할 수 있습니다.

모든 테넌트 구성 파일은 다음과 같습니다.

* 키 서버 자격 증명 - Adobe에서 발급한 하나 이상의 키 서버 자격 증명(인증서 및 개인 키)을 지정합니다. 파일 및 암호 경로 또는 HSM에 저장된 자격 증명의 별칭으로 지정할 수 있습니다. [!DNL .pfx] 파일 경로, 키 별칭 또는 둘 다 여기에서 여러 자격 증명을 지정할 수 있습니다.

iOS **테넌트** 구성 파일에는 다음이 포함됩니다.

* 키 배달 창 - (선택 사항) 키 배달 요청 타임스탬프 유효성 창(초)을 지정합니다. 기본값은 500초입니다.

Xbox **360** 테넌트 구성 파일에는 다음이 포함되어 있습니다.

* XSTS 자격 증명 - XSTS 토큰을 해독하는 데 사용되는 응용 프로그램 개발자의 자격 증명을 지정합니다.
* XSTS 서명 인증서 - XSTS 토큰에서 서명을 확인하는 데 사용되는 인증서를 지정합니다.
* Packager Whitelist - 키 서버에서 신뢰하는 패키지 인증서 목록에 포함된 패키지 인증서가 없으면 모든 패키지 인증서를 신뢰할 수 있습니다.

## 로그 파일 {#log-files}

Primetime DRM 키 서버 응용 프로그램 [!DNL flashaccess-ioskeyserver_*.log] 및 [!DNL flashaccess-xboxkeyserver_*.log]에서 생성된 로그 파일은 에서 지정한 디렉토리에 있습니다 `KeyServer.LogRoot`.

로그 파일은 클라이언트 유형별로 구분됩니다. 클라이언트 유형당 두 개의 로그가 있습니다.

* 액세스 *로그* - 요청 및 응답만 모니터링합니다.
* 컨텍스트 *로그* - 자세한 오류 메시지와 스택 추적이 포함되어 있습니다.

## 키 서버 시작 {#starting-the-key-server}

키 서버를 시작하려면 Tomcat을 시작합니다.
---
title: 보호된 스트리밍을 위한 서버 설정 및 배포
description: 보호된 스트리밍을 위한 서버 설정 및 배포
copied-description: true
exl-id: de1488e6-ccee-49e6-999e-6c6762dd55be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 보호된 스트리밍을 위한 서버 설정 및 배포 {#set-up-and-deploy-the-server-for-protected-streaming}

1. Primetime DRM DVD에서 구성 폴더를 설정합니다.

   `\Adobe Access Server for Protected Streaming\configs\`
1. 샘플 복사 `configs` 폴더를 `<Tomcat_installation_dir>` 복사된 폴더의 이름을 다음으로 바꾸기 `licenseserver`.

   이제 구성 폴더의 경로는 다음과 같아야 합니다. `<Tomcat_install_dir>\licenseserver\`.
1. 실행 `Scrambler.bat` Primetime DRM에서 전송 및 라이선스 서버 PFX 파일에 대한 암호화된 암호 얻기 `<DVD>` `\Adobe Access Server for Protected Streaming\` 디렉터리:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. PFX 파일을 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` 디렉토리.
1. 에서 해당 테넌트 구성 편집 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, 다음 설정 포함:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 실행 `Validator.bat` 구성이 유효한지 확인하는 유틸리티:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 다음을 복사합니다. `flashaccessserver.war` CD에서 `<TomcatInstallDir>\webapps\` 디렉토리.
1. Tomcat이 실행 중인 경우 를 눌러 실행 중인 Tomcat 인스턴스를 중지합니다. `<CTRL-C>` 명령 창(명령 창에서 실행된 경우)에서 Tomcat이 Windows 서비스로 설치된 경우 Windows 서비스 응용 프로그램에서 서버를 중지할 수도 있습니다.
1. Tomcat을 시작하려면 다음 명령을 입력합니다.

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 설정을 확인하려면 브라우저에 다음 URL을 입력합니다.

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```

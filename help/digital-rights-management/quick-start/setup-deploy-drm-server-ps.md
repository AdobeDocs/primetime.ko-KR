---
seo-title: 보호된 스트리밍을 위한 서버 설정 및 배포
title: 보호된 스트리밍을 위한 서버 설정 및 배포
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 보호된 스트리밍을 위한 서버 설정 및 배포 {#set-up-and-deploy-the-server-for-protected-streaming}

1. Primetime DRM DVD에서 구성 폴더를 설정합니다.

   `\Adobe Access Server for Protected Streaming\configs\`
1. 샘플 `configs` 폴더를 복사하여 `<Tomcat_installation_dir>` 복사한 폴더의 이름을 로 `licenseserver`변경합니다.

   이제 구성 폴더의 경로가 `<Tomcat_install_dir>\licenseserver\`되어야 합니다.
1. Primetime DRM `Scrambler.bat` 디렉터리에서 전송 및 라이선스 서버 PFX 파일에 대한 암호화된 암호를 가져오려면 `<DVD>` `\Adobe Access Server for Protected Streaming\` 다음을 실행하십시오.

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. PFX 파일을 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` 디렉터리에 복사합니다.
1. 다음 설정을 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`사용하여 에서 해당 테넌트 구성을 편집합니다.

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 이 `Validator.bat` 유틸리티를 실행하여 구성이 유효한지 확인합니다.

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. CD에서 `flashaccessserver.war` 파일을 `<TomcatInstallDir>\webapps\` 디렉토리로 복사합니다.
1. Tomcat이 실행 중인 경우 명령 창에서 `<CTRL-C>` 실행하는 Tomcat 인스턴스를 눌러 중지합니다(명령 창에서 실행된 경우). Tomcat이 Windows 서비스로 설치된 경우 Windows 서비스 응용 프로그램에서 서버를 중지할 수도 있습니다.
1. Tomcat을 시작하려면 다음 명령을 입력합니다.

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 설정을 확인하려면 브라우저에서 다음 URL을 입력합니다.

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```

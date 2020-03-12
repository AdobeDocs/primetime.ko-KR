---
seo-title: 구성 유효성 검사기
title: 구성 유효성 검사기
uuid: 60ebd35c-290a-4f08-9bd0-178903857149
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# 구성 유효성 검사기 {#configuration-validator}

구성 파일을 변경할 때마다 서버를 시작하기 전에 Configuration Validator 유틸리티를 실행하는 것이 좋습니다. 이 유틸리티는 요청 처리 중 오류를 일으키기 전에 대부분의 구성 오류를 조기에 감지할 수 있습니다.

유효성 검사기를 실행하려면 다음 명령을 사용합니다.

```
Validator.bat options  
```

또는 명령:

```
java -jar libs/flashaccess-validator.jar options 
```

각 라이센스 서버 구성 파일에 대해 유효성 검사기는 파일 기반 유효성 검사를 수행하여 XML 파일의 형식이 올바르고 구성 파일 스키마를 따르도록 할 수 있습니다. 전역 구성 파일에서 파일 기반 유효성 검사를 수행하려면 다음 명령을 실행합니다.

```
Validator --file path/flashaccess-global.xml --global
```

테넌트 구성 파일에서 파일 기반 유효성 검사를 수행하려면 다음 명령을 실행합니다.

```
Validator --file path/flashaccess-tenant.xml --tenant
```

또한 유효성 검사기는 배포 기반 유효성 검사를 수행할 수 있습니다.이 수준의 유효성 검사는 스키마와의 호환성을 확인하는 것 외에도 지정된 값이 유효한지 확인합니다(예: 참조된 파일이 있는지 확인). 배포 기반 유효성 검사는 다음 두 가지 수준에서 수행할 수 있습니다.

* 임차인 — 특정 테넌트에 대한 구성 파일 및 자격 증명을 검증합니다. &quot;tenant1&quot;에 대한 구성의 유효성을 확인하려면 다음 명령을 실행합니다.

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* 글로벌 — 모든 테넌트에 대한 글로벌 구성 파일 및 테넌트 유효성 검사를 확인합니다. 전역 배포 기반 유효성 검사를 수행하려면 다음 명령을 실행합니다.

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```


---
title: 구성 검사기
description: 구성 검사기
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 구성 검사기 {#configuration-validator}

Adobe은 구성 파일이 변경될 때마다 서버를 시작하기 전에 Configuration Validator 유틸리티를 실행하는 것이 좋습니다. 이 유틸리티는 대부분의 구성 오류를 조기에 감지할 수 있으며, 이 경우 요청 처리 중에 오류가 발생하기 전에 미리 감지할 수 있습니다.

유효성 검사기를 실행하려면 다음 명령을 사용합니다.

```
Validator.bat options  
```

또는 명령:

```
java -jar libs/flashaccess-validator.jar options 
```

각 라이센스 서버 구성 파일에 대해 유효성 검사기는 파일 기반 유효성 검사를 수행하여 XML 파일의 형식이 양호하고 구성 파일 스키마를 준수하는지 확인할 수 있습니다. 전역 구성 파일에서 파일 기반 유효성 검사를 수행하려면 다음 명령을 실행합니다.

```
Validator --file path/flashaccess-global.xml --global
```

테넌트 구성 파일에서 파일 기반 유효성 검사를 수행하려면 다음 명령을 실행합니다.

```
Validator --file path/flashaccess-tenant.xml --tenant
```

유효성 검사기는 배포 기반 유효성 검사도 수행할 수 있습니다. 이 유효성 검사 수준은 스키마와 일치하는지 확인하는 것 외에도 지정된 값이 유효한지 확인합니다(예: 참조된 파일이 있는지 확인). 배포 기반 유효성 검사는 다음 두 가지 수준에서 수행할 수 있습니다.

* 테넌트 — 특정 테넌트에 대한 구성 파일 및 자격 증명의 유효성을 검사합니다. &quot;tenant1&quot;에 대한 구성의 유효성을 검사하려면 다음 명령을 실행합니다.

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* 전역 — 모든 테넌트에 대한 전역 구성 파일 및 테넌트 유효성 검사를 확인합니다. 전역 배포 기반 유효성 검사를 수행하려면 다음 명령을 실행합니다.

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```

---
description: Adobe은 구성 파일을 변경할 경우 서버를 시작하기 전에 Configuration Validator 유틸리티를 실행해야 한다고 권장합니다. 이 유틸리티는 대부분의 구성 오류를 조기에 감지할 수 있으며, 이 경우 요청 처리 중에 오류가 발생하기 전에 미리 감지할 수 있습니다.
title: 구성 검사기
exl-id: 41d0a926-4e12-442c-886e-5f12cf10eed8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 구성 검사기{#configuration-validator}

Adobe은 구성 파일을 변경할 경우 서버를 시작하기 전에 Configuration Validator 유틸리티를 실행해야 한다고 권장합니다. 이 유틸리티는 대부분의 구성 오류를 조기에 감지할 수 있으며, 이 경우 요청 처리 중에 오류가 발생하기 전에 미리 감지할 수 있습니다.

검사기를 실행하려면 다음을 입력합니다.

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

또는

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

각 라이센스 서버 구성 파일에 대해 유효성 검사기는 파일 기반 유효성 검사를 수행하여 XML 파일의 형식이 양호하고 구성 파일 스키마를 준수하는지 확인할 수 있습니다.

전역 구성 파일에 대해 파일 기반 유효성 검사를 수행하려면 다음을 입력합니다.

```
Validator --<file path>/flashaccess-global.xml --global
```

테넌트 구성 파일에 대해 파일 기반 유효성 검사를 수행하려면 다음을 입력합니다.

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

유효성 검사기는 배포 기반 유효성 검사를 수행할 수도 있습니다. 이 유효성 검사 수준은 스키마와 일치하는지 확인하는 것 외에도 지정한 값이 유효한지 확인합니다. 예를 들어, 참조된 파일이 있는지 확인합니다.

배포 기반 유효성 검사는 다음 수준에서 수행할 수 있습니다.

* `Tenant` — 특정 테넌트에 대한 구성 파일 및 자격 증명의 유효성을 검사합니다. 구성에 대한 유효성을 검사하려는 경우 `<tenant1>`, 유형:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — 모든 테넌트에 대한 전역 구성 파일 및 테넌트 유효성 검사를 확인합니다. 전역 배포 기반 유효성 검사를 수행하려면 다음을 입력합니다.

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

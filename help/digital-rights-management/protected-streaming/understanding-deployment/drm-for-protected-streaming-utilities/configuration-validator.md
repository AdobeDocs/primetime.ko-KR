---
description: 구성 파일을 변경하는 경우 서버를 시작하기 전에 Configuration Validator 유틸리티를 실행해야 합니다. 이 유틸리티는 요청 처리 중 오류를 일으키기 전에 대부분의 구성 오류를 조기에 감지할 수 있습니다.
seo-description: 구성 파일을 변경하는 경우 서버를 시작하기 전에 Configuration Validator 유틸리티를 실행해야 합니다. 이 유틸리티는 요청 처리 중 오류를 일으키기 전에 대부분의 구성 오류를 조기에 감지할 수 있습니다.
seo-title: 구성 유효성 검사기
title: 구성 유효성 검사기
uuid: 7b44919a-0319-4675-95e2-ad1ad72ec0cb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 구성 유효성 검사기{#configuration-validator}

구성 파일을 변경하는 경우 서버를 시작하기 전에 Configuration Validator 유틸리티를 실행해야 합니다. 이 유틸리티는 요청 처리 중 오류를 일으키기 전에 대부분의 구성 오류를 조기에 감지할 수 있습니다.

유효성 검사기를 실행하려면 다음을 입력합니다.

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

or

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

각 라이센스 서버 구성 파일에 대해 유효성 검사기는 파일 기반 유효성 검사를 수행하여 XML 파일의 형식이 올바르고 구성 파일 스키마를 따르는지 확인할 수 있습니다.

전역 구성 파일에서 파일 기반 유효성 검사를 수행하려면 다음을 입력합니다.

```
Validator --<file path>/flashaccess-global.xml --global
```

테넌트 구성 파일에서 파일 기반 유효성 검사를 수행하려면 다음을 입력합니다.

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

유효성 검사기는 배포 기반 유효성 검사를 수행할 수도 있습니다. 이 유효성 검사 수준은 스키마와의 호환성을 확인하는 것 외에도 지정한 값이 유효한지 확인합니다. 예를 들어 참조된 파일이 있는지 확인합니다.

배포 기반 유효성 검사는 다음 수준에서 수행할 수 있습니다.

* `Tenant` — 특정 테넌트에 대한 구성 파일 및 자격 증명을 검증합니다. 구성을 검증하려면 `<tenant1>`다음을 입력합니다.

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — 모든 테넌트에 대한 글로벌 구성 파일 및 테넌트 유효성 검사를 확인합니다. 전역 배포 기반 유효성 검사를 수행하려면 다음을 입력합니다.

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```


---
description: Adobe Primetime DRM 서버에서 보호된 스트리밍 애플리케이션에 대해 생성한 로그 파일은 LicenseServer.LogRoot에서 지정한 디렉터리에 있습니다.
title: 로그 파일
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 로그 파일{#log-files}

Adobe Primetime DRM 서버에서 보호된 스트리밍 애플리케이션에 대해 생성한 로그 파일은 LicenseServer.LogRoot에서 지정한 디렉터리에 있습니다.

>[!NOTE]
>
>서버가 실행되는 동안 현재 로그 파일을 삭제하거나 이동하면 로그 파일이 다시 생성되지 않을 수 있습니다. 따라서 일부 로그 정보가 삭제될 수 있습니다.

## 로그 디렉터리 구조 {#section_F490A483D60145ADBC21038914C39203}

로그 디렉터리는 사용하기 쉽게 구조화되었습니다. 로그 디렉토리의 구조는 다음과 같습니다.

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

## 글로벌 로그 파일 {#section_1CFA90748142439C9F3BE380969539DA}

글로벌 로그 파일, `flashaccess-global.log`, 위치: *LicenseServer.Logroot*. 로그는 Adobe Primetime DRM Java SDK가 생성한 로그 메시지 또는 서버가 초기화된 시간 동안 생성된 로그 메시지를 포함할 수 있다.

## 파티션 로그 파일 {#section_5660137CD6AA40519E72A4315534846B}

파티션 로그 파일, `flashaccess-partition.log`는에 있습니다. `<LicenseServer.LogRoot>/flashaccesserver` 디렉토리. 여기에는 라이센스 요청 처리 중에 생성된 로그 메시지가 포함됩니다.

## 테넌트 로그 파일 {#section_F0257CC0831647F18A746B4F02E3E910}

각 테넌트의 테넌트 로그 파일, `flashaccess-tenant.log`, 위치: `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. 테넌트 로그에는 이 테넌트에 대해 생성된 각 라이선스를 설명하는 감사 정보가 포함됩니다.

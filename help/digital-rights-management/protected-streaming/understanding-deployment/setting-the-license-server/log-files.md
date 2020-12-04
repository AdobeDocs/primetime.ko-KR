---
description: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버에서 생성된 로그 파일은 LicenseServer.LogRoot에서 지정한 디렉토리에 있습니다.
seo-description: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버에서 생성된 로그 파일은 LicenseServer.LogRoot에서 지정한 디렉토리에 있습니다.
seo-title: 로그 파일
title: 로그 파일
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 로그 파일{#log-files}

보호된 스트리밍을 위한 Adobe Primetime DRM 서버에서 생성된 로그 파일은 LicenseServer.LogRoot에서 지정한 디렉토리에 있습니다.

>[!NOTE]
>
>서버가 실행되는 동안 현재 로그 파일을 삭제하거나 이동하는 경우 로그 파일을 다시 만들지 못할 수 있습니다. 따라서 일부 로그 정보가 삭제될 수 있습니다.

## 로그 디렉터리 구조 {#section_F490A483D60145ADBC21038914C39203}

로그 디렉토리는 사용하기 쉽게 구성됩니다. 로그 디렉토리의 구조는 다음과 같습니다.

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

## 전역 로그 파일 {#section_1CFA90748142439C9F3BE380969539DA}

전역 로그 파일 `flashaccess-global.log`은 *LicenseServer.LogRoot*&#x200B;에 있습니다. Adobe Primetime DRM Java SDK 또는 로그 메시지가 서버가 초기화된 동안 생성된 로그 메시지를 로그에 포함할 수 있습니다.

## 파티션 로그 파일 {#section_5660137CD6AA40519E72A4315534846B}

파티션 로그 파일 `flashaccess-partition.log`이(가) `<LicenseServer.LogRoot>/flashaccesserver` 디렉터리에 있습니다. 여기에는 라이센스 요청을 처리하는 동안 생성된 로그 메시지가 포함됩니다.

## 테넌트 로그 파일 {#section_F0257CC0831647F18A746B4F02E3E910}

각 테넌트의 테넌트 로그 파일 `flashaccess-tenant.log`은 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`에 있습니다. 테넌트 로그에는 이 테넌트에 대해 생성된 각 라이선스를 설명하는 감사 정보가 포함됩니다.

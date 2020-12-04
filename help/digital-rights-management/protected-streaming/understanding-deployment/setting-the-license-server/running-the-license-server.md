---
seo-title: 보호된 스트리밍을 위한 DRM 서버 실행
title: 보호된 스트리밍을 위한 DRM 서버 실행
uuid: 9bbe211d-268b-43c2-9e55-7ce62de40d30
translation-type: tm+mt
source-git-commit: 51b3713e04fcb4adeaa7a8d1b700372b1dba7cf6
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# 보호된 스트리밍을 위한 DRM 서버 실행 {#running-the-drm-server-for-protected-streaming}

보호된 스트리밍을 위한 Adobe Primetime DRM 서버를 시작하려면 먼저 구성 파일에서 설정의 유효성을 확인하는 것이 좋습니다.

라이센스 서버와 함께 제공된 유틸리티를 사용하여 설정의 유효성을 확인할 수 있습니다. 이 안내서의 *구성 유효성 검사기*&#x200B;를 참조하십시오.

Tomcat 및 라이센스 서버를 시작하려면 Tomcat의 [!DNL bin] 디렉토리에서 [!DNL catalina.bat start] 또는 [!DNL catalina.sh start]을 실행해야 합니다.

서버가 시작된 후 브라우저 창에서 `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1`을(를) 열어 서버가 올바르게 구성되었는지 확인해야 합니다. 테넌트 구성이 성공적으로 로드되면 확인 메시지가 나타납니다.

## 로그 파일 {#log-files}

보호된 스트리밍을 위한 Adobe Primetime DRM 서버에서 생성된 로그 파일은 LicenseServer.LogRoot에서 지정한 디렉토리에 있습니다.

>[!NOTE]
>
>서버가 실행되는 동안 현재 로그 파일을 삭제하거나 이동하는 경우 로그 파일을 다시 만들지 못할 수 있습니다. 따라서 일부 로그 정보가 삭제될 수 있습니다.

### 로그 디렉터리 구조 {#section_F490A483D60145ADBC21038914C39203}

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

### 전역 로그 파일 {#section_1CFA90748142439C9F3BE380969539DA}

전역 로그 파일 [!DNL flashaccess-global.log]은 *LicenseServer.LogRoot*&#x200B;에 있습니다. Adobe Primetime DRM Java SDK 또는 로그 메시지가 서버가 초기화된 동안 생성된 로그 메시지를 로그에 포함할 수 있습니다.

### 파티션 로그 파일 {#section_5660137CD6AA40519E72A4315534846B}

파티션 로그 파일 [!DNL flashaccess-partition.log]이(가) `<LicenseServer.LogRoot>/flashaccesserver` 디렉터리에 있습니다. 여기에는 라이센스 요청을 처리하는 동안 생성된 로그 메시지가 포함됩니다.

### 테넌트 로그 파일 {#section_F0257CC0831647F18A746B4F02E3E910}

각 테넌트의 테넌트 로그 파일 [!DNL flashaccess-tenant.log]은 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`에 있습니다. 테넌트 로그에는 이 테넌트에 대해 생성된 각 라이선스를 설명하는 감사 정보가 포함됩니다.

## 구성 파일 {#updating-configuration-files} 업데이트

라이센스 서버가 라이센스 서버 구성 파일 중 하나를 읽으면(글로벌 또는 테넌트 구성) 구성 정보가 메모리에 캐시됩니다. 따라서 라이센스 요청마다 파일을 디스크에서 읽을 필요가 없습니다. 그러나 변경 사항을 적용하기 위해 서버를 다시 시작할 필요 없이 구성 파일의 대부분의 값을 수정할 수도 있습니다.

구성 파일을 수정할 때마다 라이센스 서버는 파일을 마지막으로 수정한 시간을 저장합니다. 구성 가능한 간격으로 서버는 파일 수정 시간이 변경되었는지 확인합니다. 변경된 경우 서버가 구성 파일의 내용을 자동으로 다시 로드합니다.

서버에서 업데이트를 확인하는 빈도를 제어하려면 전역 구성 파일의 `Caching` 요소에서 `refreshDelaySeconds` 특성을 설정해야 합니다. 예를 들어 `refreshDelaySeconds`이 3600초로 설정된 경우 서버는 구성 파일의 수정 시간으로부터 최대 1시간 내에 구성을 업데이트합니다. `refreshDelaySeconds`이 0으로 설정된 경우 서버는 모든 요청에서 구성 업데이트를 확인합니다. 이렇게 하면 성능에 영향을 줄 수 있으므로 제작 환경에서 `refreshDelaySeconds`을(를) 낮은 값으로 설정하는 것이 좋습니다.

`Caching` 요소는 동시에 캐시되는 테넌트 구성 수도 제어합니다. 이 값을 총 테넌트 수보다 작은 수로 설정하여 구성 정보를 캐시하는 데 사용되는 메모리 양을 제한할 수 있습니다. 캐시에 없는 테넌트에 대한 요청이 수신되면 요청이 처리되기 전에 구성이 로드됩니다. 캐시가 가득 찬 경우 최근에 사용한 테넌트 이 캐시에서 제거됩니다.

캐시된 구성 버전은 다음 상황에서 계속 사용됩니다(다음 번에 서버가 업데이트를 확인할 때까지).

* 서버가 파일 읽기를 시도하는 동안 구성 파일 또는 [!DNL flashaccess-tenant.xml] 파일에서 참조되는 인증서 파일에 변경 사항이 저장되는 경우
* 파일의 타임스탬프가 현재 시간 1초 미만이면
* 파일의 타임스탬프가 향후

캐시된 버전이 없으면 구성을 로드하지 못하고 오류가 클라이언트에 반환됩니다. 그런 다음 서버는 다음에 해당 테넌트에 대한 요청을 받을 때 파일을 다시 로드합니다.

### 전역 구성 파일 {#section_AA546C72442646CFB8906AEEBDF50587} 업데이트

[!DNL flashaccess-global.xml]에서 HSM 암호를 언제든지 수정할 수 있습니다. 변경 사항은 다음에 서버가 구성 파일을 다시 로드할 때 적용됩니다. 하지만 로깅 및 캐싱 요소의 변경 사항은 다시 로드되지 않습니다. 이러한 요소에 대한 변경 사항이 적용되기 전에 서버를 다시 시작해야 합니다.

### 테넌트 구성 파일 {#section_71624DB8DF28480F84F34F0FF7FD4365} 업데이트

[!DNL flashaccess-tenant.xml] 파일에 지정된 모든 값을 언제든지 수정할 수 있습니다. 변경 사항은 다음에 서버가 구성 파일을 다시 로드할 때 적용됩니다. 또한 서버는 테넌트 구성 파일에서 참조되는 모든 자격 증명( [!DNL .pfx]) 파일 및 패키지 허용 목록 인증서 파일의 수정을 확인합니다.
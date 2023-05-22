---
title: 보호된 스트리밍을 위한 DRM 서버 실행
description: 보호된 스트리밍을 위한 DRM 서버 실행
copied-description: true
exl-id: 05dc4c55-a97e-4bdc-aea8-32741299454c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 보호된 스트리밍을 위한 DRM 서버 실행 {#running-the-drm-server-for-protected-streaming}

보호된 스트리밍을 위해 Adobe Primetime DRM 서버를 시작하려면 구성 파일에서 설정의 유효성을 확인하는 것이 좋습니다.

라이센스 서버와 함께 제공된 유틸리티를 사용하여 설정의 유효성을 확인할 수 있습니다. (참조: *구성 검사기* 이 안내서에서 참조하십시오.

Tomcat과 라이센스 서버를 시작하려면 다음을 실행해야 합니다 [!DNL catalina.bat start] 또는 [!DNL catalina.sh start] Tomcat에서 [!DNL bin] 디렉토리.

서버가 시작된 후에는 를 열어 서버가 올바르게 구성되었는지 확인해야 합니다 `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` 을 클릭합니다. 테넌트 구성이 성공적으로 로드되면 확인 메시지가 나타납니다.

## 로그 파일 {#log-files}

Adobe Primetime DRM 서버에서 보호된 스트리밍 애플리케이션에 대해 생성한 로그 파일은 LicenseServer.LogRoot에서 지정한 디렉터리에 있습니다.

>[!NOTE]
>
>서버가 실행되는 동안 현재 로그 파일을 삭제하거나 이동하면 로그 파일이 다시 생성되지 않을 수 있습니다. 따라서 일부 로그 정보가 삭제될 수 있습니다.

### 로그 디렉터리 구조 {#section_F490A483D60145ADBC21038914C39203}

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

### 글로벌 로그 파일 {#section_1CFA90748142439C9F3BE380969539DA}

글로벌 로그 파일, [!DNL flashaccess-global.log], 위치: *LicenseServer.Logroot*. 로그는 Adobe Primetime DRM Java SDK가 생성한 로그 메시지 또는 서버가 초기화된 시간 동안 생성된 로그 메시지를 포함할 수 있다.

### 파티션 로그 파일 {#section_5660137CD6AA40519E72A4315534846B}

파티션 로그 파일, [!DNL flashaccess-partition.log]는에 있습니다. `<LicenseServer.LogRoot>/flashaccesserver` 디렉토리. 여기에는 라이센스 요청 처리 중에 생성된 로그 메시지가 포함됩니다.

### 테넌트 로그 파일 {#section_F0257CC0831647F18A746B4F02E3E910}

각 테넌트의 테넌트 로그 파일, [!DNL flashaccess-tenant.log], 위치: `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. 테넌트 로그에는 이 테넌트에 대해 생성된 각 라이선스를 설명하는 감사 정보가 포함됩니다.

## 구성 파일 업데이트 중 {#updating-configuration-files}

라이센스 서버가 라이센스 서버 구성 파일(전역 또는 테넌트 구성) 중 하나를 읽는 즉시 구성 정보가 메모리에 캐시됩니다. 따라서 모든 라이센스 요청에 대해 디스크에서 파일을 읽을 필요가 없습니다. 단, 변경 사항을 적용하기 위해 서버를 다시 시작하지 않아도 구성 파일의 대부분의 값을 수정할 수 있습니다.

구성 파일을 수정할 때마다 라이센스 서버는 파일이 마지막으로 수정된 시간을 저장합니다. 구성 가능한 간격으로 서버는 파일 수정 시간이 변경되었는지 확인합니다. 변경된 경우 서버는 구성 파일의 내용을 자동으로 다시 로드합니다.

서버가 업데이트를 확인하는 빈도를 제어하려면 `refreshDelaySeconds` 의 속성 `Caching` 전역 구성 파일의 요소입니다. 예를 들어 다음과 같습니다. `refreshDelaySeconds` 이 3,600초로 설정되면 서버는 구성 파일의 수정 시간으로부터 최대 1시간 이내에 구성을 업데이트합니다. If `refreshDelaySeconds` 이 0으로 설정되면 서버는 모든 요청 시 구성 업데이트를 확인합니다. 설정하지 않는 것이 좋습니다 `refreshDelaySeconds` 이렇게 하면 성능에 영향을 줄 수 있으므로 모든 프로덕션 환경에서 낮은 값으로 유지됩니다.

다음 `Caching` 또한 요소는 한 번에 캐시되는 테넌트의 구성 수를 제어합니다. 이 값을 전체 테넌트 수보다 작은 수로 설정하여 구성 정보를 캐시하는 데 사용되는 메모리 양을 제한할 수 있습니다. 캐시에 없는 테넌트에 대해 요청을 받으면 요청이 처리되기 전에 구성이 로드됩니다. 캐시가 가득 차면 가장 최근에 사용된 테넌트가 캐시에서 제거됩니다.

구성의 캐시된 버전은 다음 상황에서 계속 사용됩니다(다음에 서버가 업데이트를 확인할 때까지).

* 변경 사항을 구성 파일이나 [!DNL flashaccess-tenant.xml] 서버가 파일을 읽으려고 시도하는 동안 파일
* 파일의 타임스탬프가 현재 시간보다 1초 미만인 경우
* 파일의 타임스탬프가 미래인 경우

캐시된 버전이 없으면 구성 로드가 실패하고 클라이언트에 오류가 반환됩니다. 그런 다음 서버는 다음에 해당 테넌트에 대한 요청을 수신할 때 파일 로드를 다시 시도합니다.

### 전역 구성 파일 업데이트 {#section_AA546C72442646CFB8906AEEBDF50587}

에서 HSM 암호를 수정할 수 있습니다. [!DNL flashaccess-global.xml] 언제든지. 변경 사항은 다음에 서버가 구성 파일을 다시 로드할 때 적용됩니다. 하지만 로깅 및 캐싱 요소에 대한 변경 사항은 다시 로드되지 않습니다. 이러한 요소에 대한 변경 사항이 적용되기 전에 서버를 다시 시작해야 합니다.

### 테넌트 구성 파일 업데이트 {#section_71624DB8DF28480F84F34F0FF7FD4365}

에 지정된 모든 값을 수정할 수 있습니다. [!DNL flashaccess-tenant.xml] 언제든지 파일에 액세스할 수 있습니다. 변경 사항은 다음에 서버가 구성 파일을 다시 로드할 때 적용됩니다. 또한 서버는 모든 자격 증명의 수정 사항을 확인합니다( [!DNL .pfx]) 테넌트 구성 파일에서 참조되는 파일 및 packager 허용 목록 인증서 파일.

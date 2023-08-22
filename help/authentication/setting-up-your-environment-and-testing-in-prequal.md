---
title: 사전 영업 시 환경 설정 및 테스트
description: 사전 영업 시 환경 설정 및 테스트
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 환경을 설정 하 고 사전에 테스트{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>이 페이지의 컨텐츠은 정보 제공 목적 으로만 제공 됩니다. 이 API를 사용 하려면 Adobe Systems에서 현재 라이센스가 필요 합니다. 무단 사용은 허용 되지 않습니다.

이 기술 메모의 목적은 파트너가 환경을 설정 하 고 Adobe Systems 사전 자격 부여 환경에 배포 된 새 빌드 테스트를 시작 하는 데 있습니다.

두 가지 빌드 특색이 있기 때문입니다. ****** ****** 이 포커스 문서에서 프로덕션 설정에는 모든 단계를 스테이징에 동일 하 게 동일 하 게 설명 하 고, url만 다릅니다.

1 단계와 2 단계는 테스트 컴퓨터 중 하나에서 테스트 환경을 설정 하는 것입니다. 3 단계는 기본 흐름을 확인 하 고 4 &amp; 5 단계는 일부 테스트 지침을 제공 합니다.

>[!IMPORTANT]
>
> 테스트 환경을 변경 하려고 할 때마다 1 단계와 2 단계를 실행 하는 것이 매우 중요 합니다 (스테이징에서 프로덕션 프로필로 또는 다른 방법으로 전환).


## 1단계. IP에 도메인 전달 확인 {#resolving-pass-domain-to-an-ip}

* 스푸핑에 사용할 수 있는 로드 밸런서 IP를 찾으려면 다음 명령을 실행합니다.

* **Windows**

  ```cmd
  C:\>nslookup sp-prequal.auth.adobe.com
  ...
  Addresses:  52.13.71.11
              54.184.208.150
  ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **Linux/Mac에서**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>답변에서 제외 되는 도메인은 관련이 없고 사용자 사용자와 다를 수 있습니다.

>[!IMPORTANT]
>
> 이러한 IP 주소는 나중에 변경 될 수 있으며 지리적으로 다른 지역의 사용자에 대해 동일 하지 않을 수 있습니다.


## 2 단계.  사전 자격이 있는 환경을 프로덕션으로 스푸핑 {#spoofing-the-prequalification-environment}

* *C:\\windows\\System32\\drivers\\etc\\hosts* 파일 (windows) 또는 */Etc/hosts* 파일 (Macintosh/Linux/Android)을 편집 하 고 다음을 추가 합니다.

* 스푸핑 프로덕션 프로필
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Android에서 스푸핑:** Android에서 스푸핑하려면 Android 에뮬레이터를 사용해야 합니다.

* 스푸핑이 적용되면 프로덕션 및 스테이징 프로필에 일반 URL을 사용할 수 있습니다(즉, `http://sp.auth-staging.adobe.com` 및 `http://entitlement.auth-staging.adobe.com` 그리고 당신은 실제로 *사전 검증 환경/프로덕션* * 새로운 빌드.


## 3단계.  올바른 환경을 가리키는지 확인합니다. {#Verify-you-are-pointing-to-the-right-environment}

**이는 쉬운 단계입니다.**

* 권한 부여 prequal 환경 ](https://entitlement-prequal.auth.adobe.com/environment.html) 및 자격 ](https://entitlement.auth.adobe.com/environment.html) 을 [ 로드 [ 합니다. 동일한 응답을 반환 해야 합니다.


## 4 단계.  프로그래머용 웹 사이트를 사용 하 여 간단한 인증/인증 흐름 수행 {#peform-a-simple-auth-flow}

* 이 단계에는 프로그래머의 웹 사이트 주소와 일부 유효한 MVPD 자격 증명 사용자 (인증 및 권한 부여 됨)이 필요 합니다.

## 5 단계.  프로그래머의 웹 사이트를 사용 하 여 시나리오 테스트 수행 {#perform-scenario-testing-using-programmer-website}

* 환경 설정을 완료 하 고 기본 인증-권한 부여 흐름이 작동 하는지 확인 한 후 보다 복잡 한 시나리오 테스트를 진행할 수 있습니다.


## 6단계.  API 테스트 사이트를 사용하여 테스트 수행 {#perform-testing-using-api-testing-site}

* Adobe Primetime 인증 테스트에 더 자세히 알아보려면 [API 테스트 사이트](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

API 테스트 사이트에 대한 자세한 내용은 다음 위치에서 확인할 수 있습니다. [Adobe의 API 테스트 사이트를 사용하여 인증 및 권한 부여 흐름을 테스트하는 방법](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

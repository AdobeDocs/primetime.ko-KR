---
title: Primetime 인증 지표에서 Clientless deviceType 매개 변수를 사용하는 것의 이점
description: Primetime 인증 지표에서 Clientless deviceType 매개 변수를 사용하는 것의 이점
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Primetime 인증 지표에서 Clientless deviceType 매개 변수를 사용하는 것의 이점 {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>

## 컨텍스트

선택 사항이지만 매개 변수는 `deviceType` clientless API가 있을 경우 를 통해 노출되는 Primetime 인증 지표에 사용합니다 [자격 서비스 모니터링](/help/authentication/entitlement-service-monitoring-overview.md).

그 사이에 `deviceType` 매개 변수 및 해당 **이점** Primetime 인증 지표가 처음에 언급되지 않은 경우 이 기술 노트의 범위는 지표에 대한 추가 정보를 추가하는 것입니다.

## 설명

다음 `deviceType` 첫 번째 버전 이후 Clientless API에 매개 변수가 있지만 최신 릴리스에서 Primetime 인증 지표에 대한 의미가 추가되었습니다.



>[!IMPORTANT]
>
>매개 변수가 `deviceType` 이 올바르게 설정되면 다음 항목이 있습니다 **혜택** 권한 부여 서비스 모니터링에서: 이 템플릿은 다음과 같은 지표를 제공합니다 [장치 유형별 분류](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.


Entitlement Service Monitoring API에 대한 자세한 내용은 [드릴 다운 트리,](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) 다음을 나타냅니다 [차원](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) (리소스) ESM 2.0에서 사용할 수 있습니다.

>[!NOTE]
>
>이 기술 노트의 컨텐츠는 [Clientless API](#clientless_device_type).




## 구현

Primetime 인증 지표를 최대한 활용하려면 두 가지 유형이 있습니다 [Clientless API](#web_srvs_summary) 현재 사용 중이며 올바른 정보가 필요합니다. `deviceType` 설정:

1. 가 있는 API `regcode` 를 필수 매개 변수로 사용하고 `deviceType` 매개 변수를 만들 때 설정합니다. `regcode`를 설정하는 것이 좋습니다.
   - [\&lt;reggie _fqdn=&quot;&quot;>/regie/v1/{requestorId}/regcode](#reg_serv)

1. 가 있는 API `deviceType` 선택적 매개 변수로:
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorization](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediattoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorization](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

당사의 권장 사항은 `deviceType` 매개 변수를 설정하고 모든 API에 대한 올바른 Clientless 장치 유형을 전달합니다.



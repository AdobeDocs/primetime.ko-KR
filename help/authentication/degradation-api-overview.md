---
title: 성능 저하 API 개요
description: 성능 저하 API 개요
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 성능 저하 API 개요 {#degradation-api-overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 일반 정보 {#general_info}

>[!NOTE]
>
>이 API는 일반적으로 사용할 수 없습니다. 가용성 업데이트에 대해서는 Adobe 담당자에게 문의하십시오.

이 기능은 특정 MVPD 인증 및 인증 끝점을 일시적으로 우회하는 기능을 사용하여 통합(프로그래머, MVPD 및 Adobe)의 세 당사자 중 하나를 제공합니다. 일반적으로 이러한 작업을 수행하는 프로그래머가 되지만, 분해 이벤트를 트리거하는 사람에 관계없이, 영향을 받는 MVPD와의 계약에 따라 이전에 동의한 내용에 따라 작업이 수행됩니다.

이 기능의 기본 사용 사례는 라이브 스포츠 또는 대규모 이벤트 중에 발생합니다. 이러한 높은 트래픽 시나리오에서 특정 MVPD 종단점의 로드가 너무 많아져서 사용자에 대한 응답 시간이 매우 오래 걸릴 수 있습니다. 이러한 시나리오 동안 사용자 환경을 보존하기 위해 프로그래머는 일시적으로 사용자를 자동 인증/자동 인증할 수 있는 열화 규칙을 트리거하거나 사용 가능한 MVPD 목록에서 MVPD를 제거하여 MVPD를 비활성화할 수 있습니다.

열화 규칙은 고정된 기간 동안에만 적용됩니다. 이 기능의 기본 고객은 스포츠 채널과 라이브 뉴스 채널이지만, MVPD 서비스가 가끔 중단되므로 모든 프로그래머는 이 기능에 액세스하고 싶을 수 있습니다.

분해 참고 사항:

* 이 기능은 MVPD당 인증 및 권한 수, 평균 인증 지연 및 전체 서비스 개요에 필요한 기타 지표에 대한 실시간 정보를 제공하는 사용 모니터링 API와 함께 사용하도록 설계되었습니다.
* 이 기능을 사용하면 Adobe Primetime 인증 서비스를 건너뛸 수 없습니다. Primetime 인증이 서비스 내에 사용자가 컨텐츠를 볼 수 있도록 하는 데 사용할 수 있는 메커니즘이 없는 경우 그러나 사이트 또는 앱은 자체적으로 Primetime 인증을 라우팅할 수 있습니다.
* Adobe은 현재 열화를 직접 트리거하지 않습니다. 이 결정은 항상 MVPD와 이러한 조건에 동의한 특정 프로그래머와 함께 있어야 합니다. 앞으로 MVPD와 계약(SLA 보호)에 도달할 수 있는 경우 Primetime 인증이 성능 저하 규칙을 트리거하는 데 사전 대응될 수 있습니다.

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
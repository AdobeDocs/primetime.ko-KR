---
title: 자격 부여 서비스 모니터링 개요
description: 자격 부여 서비스 모니터링 개요
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# 자격 부여 서비스 모니터링 개요 {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#introduction}

TVE 사이트 및 앱은 24/7이 있어야 하므로 고객은 가능한 한 빨리 문제를 감지하고 수정하기 위해 자격 부여 이벤트에 대한 실시간 통찰력을 필요로 합니다. 대부분의 트래픽을 제공하고 있으며 구현이 잘못되고 전환율이 낮은 플랫폼을 판별하려면 월별 데이터를 분석해야 합니다.

ESM(Entitlement Service Monitoring)은 프로그래머 및 MVPD에게 인증 및 권한 부여 이벤트에 대한 실시간 가시성을 제공하는 데이터 피드를 제공합니다. 데이터는 Adobe Primetime 인증 시스템에서 수집되고 RESTful API를 통해 제공됩니다.  고객은 직접 또는 사용자 정의 설치 운영 대시보드 내에서 데이터를 사용할 수 있습니다.

ESM 시스템의 핵심 요소는 지표 및 차원입니다. ESM은 차원 선택에 따라 집계된 지표를 포함하는 보고서를 생성합니다. Adobe Pass 이벤트가 PST 시간대에 기록되므로 ESM 보고서는 PST 시간대에서도 사용할 수 있습니다. 

ESM API는 일반적으로 사용할 수 없습니다.  가용성에 대한 질문이 있으면 Adobe 담당자에게 문의하십시오.

## 프로그래머용 ESM {#esm-for-programmers}

### 프로그래머는 다음 지표를 모니터링할 수 있습니다. {#programmers-monitor-metrics}


| *지표 이름* | *설명* |
|-------------------------|--------------------------|
| 인증 시도 | 시작된 인증 흐름 수 |
| authn-successful | 클라이언트에서 성공적으로 얻은 인증 토큰 수 |
| 인증 보류 중 | 성공적으로 생성된 인증 토큰 수(클라이언트가 실제로 얻었는지 여부에 상관없이) |
| authn 실패 | 외부 시스템을 통해 수행된 실패한 인증 수입니다. |
| clientless tokens | 성공적으로 내보낸 클라이언트 없는 토큰 수 |
| clientless failures | Clientless API에서 토큰을 수신하려고 시도하는 동안 실패한 시도 횟수 |
| authz 시도 | 시도 권한 수 |
| authz 성공 | 성공한 권한 수 |
| authz 실패 | 응용 프로그램 수준에서 MVPD가 거부한 권한 수 |
| authz 거부 | Adobe 서비스 공급자가 DoS 공격 방지로 인해 악의적인 것으로 간주하여 거부한 승인 시도 횟수 |
| authz 지연 | MVPD의 종단점에서 보낸 총 시간(밀리초) |
| media-tokens | 생성된 짧은 미디어 토큰 수(재생 요청 수에 부합함) |
| 고유 계정 | 선택한 시간 간격에서 권한(AuthN / AuthZ) 작업을 수행한 고유 사용자 수입니다. (이 지표는 일별 값이 요청되는 경우에만 표시됩니다.) </br> 이것은 각 개별 데이터 센터에 대해 계산됩니다. &quot;dc&quot; 차원이 요청되지 않으면 이 지표가 표시되지 않습니다. |
| 고유 세션 | 선택한 시간 간격 내에 Adobe Primetime 인증 서비스에 대한 인증 흐름 호출을 수행한 고유 세션 수입니다. (이 지표는 일별 값이 요청되는 경우에만 표시됩니다.) </br> 이것은 각 개별 데이터 센터에 대해 계산됩니다. &quot;dc&quot; 차원이 요청되지 않으면 이 지표가 표시되지 않습니다. |
| count | 이벤트 기반 보고서에 사용되는 간단한 카운터 |

</br>

### 프로그래머는 다음 차원으로 위에 나열된 지표를 필터링할 수 있습니다. {#progr-filter-metrics}


| *Dimension 이름* | *설명* |
|---|---|
| 년 | 4자리 연도 |
| 월 | 월(1-12) |
| 일 | 날짜(1-31) |
| 시간 | 시간(일 기준) |
| 분 | 시간(분) |
| 미디어 회사 | 사용자에 대한 자격 프로세스를 시작한 웹 사이트를 소유한 미디어 회사입니다 |
| dc | (데이터 센터) 요청을 받은 홈 영역입니다. |
| 프록시 | 프록시 MVPD(직접 통합을 위해 &quot;직접&quot;) |
| mvpd | 사용자에게 자격 부여 업무를 담당하는 MVPD |
| requestor-id | 자격 요청을 수행하는 데 사용되는 요청자 ID입니다 |
| channel | 리소스 필드에서 추출된 채널 웹 사이트입니다(제공된 경우 MRSS 페이로드에서 채널/제목으로 추출되거나 RSS 형식이 아닌 경우 리소스 값에 매핑됨). |
| resource-id | 권한 부여 요청에 관련된 실제 리소스 제목(제공된 경우 MRSS 페이로드에서 항목/제목으로 추출) |
| 디바이스 | 장치 플랫폼(PC, 모바일, 콘솔 등)은 |
| eap | 외부 시스템을 통해 인증 흐름이 수행될 때 외부 인증 공급자입니다. </br> 값은 다음과 같습니다. </br> - N/A - Primetime 인증에서 인증을 제공했습니다 </br> - Apple - 인증을 제공한 외부 시스템은 Apple입니다 |
| os-family | 장치에서 실행 중인 운영 체제 |
| 브라우저 제품군 | Adobe Primetime 인증에 액세스하는 데 사용되는 사용자 에이전트 |
| cdt | 현재 Clientless에 사용되는 장치 플랫폼(대체 요소). </br>  값은 다음과 같습니다. </br> - N/A - 이벤트가 Clientless SDK에서 발생하지 않음 </br> - 알 수 없음 - Clientless API의 deviceType 매개 변수는 선택 사항이므로 값을 포함하지 않는 호출이 있습니다. </br> - Clientless API를 통해 전송된 다른 값(예: xbox, appletv, roku 등) </br> |
| platform-version | Clientless SDK 버전 |
| os형 | 장치에서 실행 중인 운영 체제, 대체(현재 사용되지 않음) |
| browser-version | 사용자 에이전트 버전 |
| sdk 유형 | 사용된 클라이언트 SDK(Flash, HTML5, Android 기본, iOS, Clientless 등)는 |
| sdk-version | Adobe Primetime 인증 클라이언트 SDK의 버전 |
| 이벤트 | Adobe Primetime 인증 이벤트 이름 |
| 이유 | Adobe Primetime 인증에서 보고한 실패 이유 |
| sso 유형 | 기본 SSO 메커니즘: platform/passive/adobe 다른 응용 프로그램에서 AuthN을 다시 사용하여 인증 토큰이 발생했음을 나타냅니다 |

## MVPD용 ESM {#esm-for-mvpds}

### MVPD는 다음 지표를 모니터링할 수 있습니다.

| *지표 이름* | *설명* |
|---|---|
| 인증 시도 | 시작된 인증 흐름 수 |
| authn-successful | 클라이언트에서 성공적으로 얻은 인증 토큰 수 |
| 인증 보류 중 | 성공적으로 생성된 인증 토큰 수(클라이언트가 실제로 얻었는지 여부에 상관없이) |
| authn 실패 | 외부 시스템을 통해 수행된 실패한 인증 수입니다. |
| authz 시도 | 시도 권한 수 |
| authz 성공 | 성공한 권한 수 |
| authz 실패 | 응용 프로그램 수준에서 MVPD가 거부한 권한 수 |
| authz 거부 | Adobe 서비스 공급자가 DoS 공격 방지로 인해 악의적인 것으로 간주하여 거부한 승인 시도 횟수 |
| authz 지연 | MVPD의 종단점에서 보낸 총 시간(밀리초) |

### MVPD는 다음 차원으로 위에 나열된 지표를 필터링할 수 있습니다.

| *Dimension 이름* | *설명* |
|---|---|
| 년 | 4자리 연도 |
| 월 | 월(1-12) |
| 일 | 날짜(1-31) |
| 시간 | 시간(일 기준) |
| 분 | 시간(분) |
| requestor-id | 자격 요청을 수행하는 데 사용되는 요청자 ID입니다 |
| eap | 외부 시스템을 통해 인증 흐름이 수행될 때 외부 인증 공급자입니다. </br> 값은 다음과 같습니다. </br> - N/A - Primetime 인증에서 인증을 제공했습니다 </br> - Apple - 인증을 제공한 외부 시스템은 Apple입니다 |
| cdt | 현재 Clientless에 사용되는 장치 플랫폼(대체 요소). </br>  값은 다음과 같습니다. </br> - N/A - 이벤트가 Clientless SDK에서 발생하지 않음 </br> - 알 수 없음 - Clientless API의 deviceType 매개 변수는 선택 사항이므로 값을 포함하지 않는 호출이 있습니다. </br> - Clientless API를 통해 전송된 다른 값(예: xbox, appletv, roku 등) </br> |
| sdk 유형 | 사용된 클라이언트 SDK(Flash, HTML5, Android 기본, iOS, Clientless 등)는 |


## 사용 사례 {#use-cases}

다음과 같은 사용 사례에 ESM 데이터를 사용할 수 있습니다.

- **모니터링** - Ops 또는 monitoring 팀은 매 분마다 API를 호출하는 대시보드 또는 차트를 만들 수 있습니다. 표시된 정보를 사용하여 표시되는 순간에 문제(Primetime 인증 또는 MVPD 포함)를 감지할 수 있습니다.  

- **디버깅/품질 테스트** - 데이터는 플랫폼, 장치, 브라우저 및 OS별로 분류되므로 사용 패턴을 분석하면 특정 조합(예: OSX의 Safari)에 대한 문제를 찾아낼 수 있습니다.  

- **Analytics** - 제공된 데이터는 Adobe Analytics 또는 다른 분석 도구를 통해 수집 중인 클라이언트측 데이터를 보완하거나 감사하는 데 사용할 수 있습니다.

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
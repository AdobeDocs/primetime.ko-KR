---
title: 에스컬레이션 절차
description: 에스컬레이션 절차
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 에스컬레이션 절차 {#escalation-procedures}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

>[!IMPORTANT]
> 
>핫라인 호출 : **+1-205-693-9813** 및 **tve-support@adobe.com** 포함 **긴급 - 사고** 제목 줄에서

## 소개 {#introduction}

이 문서에서는 주요 인시던트에 대한 지원 절차에 대해 설명합니다(**심각도 1** level) Adobe Primetime 인증에 영향을 주는 Primetime Concurrency Monitoring 및 해당 파트너\
 

## SEVERITY 1 레벨 인시던트 정의 {#definition-of-a-severity-1-level-incident}

A **심각도 1** 수준 인시던트는 **라이브** 상황 **프로덕션 환경에서 발생하는 문제**&#x200B;를 지정하는 경우, 한 채널과 하나의 MVPD에 대한 인증 및/또는 인증 흐름이 완료되지 않고, 이 흐름을 수행하는 MVPD의 가입자의 수가 너무 많습니다.


## SEVERITY 1 장애 예 {#examples-of-severity-1-incidentcs}

* 에서 호스팅되는 운영 Access Enabler  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` 또는 `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`)을 사용할 수 없습니다.

* 특정 MVPD의 경우 사용자가 MVPD를 선택하면 Adobe이 더 이상 로그인 페이지를 리디렉션/표시하지 않습니다(지원되는 모든 브라우저에서).

* 파트너는 사용자가 특정 MVPD로 인증/인증할 수 없는 많은 보고서를 받습니다.

* 인증 프로세스 중에 사용자가 인증/인증 흐름을 다시 시작할 수 없는 Adobe 오류 페이지에서 정지 상태가 됩니다.


| 예 **NOT** 심각도 1 사고 |
|---|
| 이러한 유형의 문제에 대해 Adobe은 조사를 지원하지만 심각도 1 사건은 아닙니다.<ul><li>Flash 버전 문제(Flash 누락, Flash 차단기, 잘못된 Flash 버전)로 인해 하나 이상의 구독자가 흐름을 수행할 수 없습니다.</li><li>한 명 또는 몇 명의 구독자가 인증하고 MVPD 로그인 페이지에 유지할 수 없습니다.</li><li>하나 이상의 구독자가 인증되었지만 비디오를 재생할 수 없습니다.</li><li>프로그래머 사이트에서 JavaScript 오류가 하나/둘/모두 발생합니다</li></ul> |

## 심각도 1 에스컬레이션 흐름 {#severity-1-escalation-flows}

심각도 1 인시던트는 Adobe 또는 Adobe Primetime 인증 파트너에 의해 시작될 수 있습니다. 각 단계에 대한 설명은 아래에 나와 있습니다.

### 파트너가 시작한 흐름 {#partner-initiated-flow}

1. 파트너는 Adobe의 즉각적인 주의가 필요한 심각도 1 사고(위에서 설명한 대로)를 식별합니다.
1. 파트너가 **tve-support@adobe.com** 포함 **긴급 - 사고** 제목 줄에서 다음 정보를 추가합니다.
   * 제목
   * 재현할 설명 및 단계
   * OS / 브라우저
   * SDK 및 버전
   * 영향을 받는 장치
   * 영향을 받는 사용자 수
   * 문제를 보여주는 HTTP 추적 또는 장치 로그
   * (선택 사항) 문제를 보여주는 모든 스크린샷 또는 비디오 캡쳐
1. Adobe이 30분 내에 티켓에 응답하지 않으면 파트너가 다음 번호를 호출합니다.
   **1-205-693-9813**

   >[!IMPORTANT]
   >티켓 제목에 &quot;긴급 사고&quot;를 포함하지 않으면 알림 시스템에서 선택하지 않습니다**.

### Adobe 시작 흐름 {#adobe-initiated-flow}

#### ...Adobe Primetime 인증 문제 {#adobe-initiated-flow-authn-issue}

1. Adobe은 내부 문제를 식별하고 추적 시스템으로 티켓을 엽니다.

1. Adobe은 파트너의 프로그램 관리자 및 기술 담당자에게 알리며 티켓 번호와 문제의 예상 영향을 지정합니다.

1. Adobe은 사고 해결을 위해 작동하며 영향을 받는 모든 파트너에게 정보를 제공합니다.

#### ...파트너 문제(프로그래머/MVPD)에 대한 {#adobe-initiated-flow-partner-issue}

1. Adobe이 MVPD와의 통합 또는 프로그래머 사이트 중 하나에서 발생하는 문제를 식별합니다.

1. Adobe은 영향을 받은 파트너에게 알립니다 <u>해당 파트너와 적절한 지원 절차 수행</u> 및 는 파트너의 지원 조직과 함께 티켓을 엽니다.

1. 영향 분석 중에 Adobe이 문제가 사고 시나리오에 대해 사전에 합의된 결정 중 하나에 속한다고 판단하는 경우 다음을 참조하십시오. **사고 시나리오에 대한 사전 합의된 결정**&#x200B;의 경우, 파트너의 입력을 기다리지 않고 적절하게 작동합니다.

1. Adobe은 서비스가 복원될 때 파트너의 업데이트와 파트너의 알림을 기다립니다.

## 사고 시나리오에 대한 사전 합의된 결정 {#pre-agreed-descn}

시나리오가 발생할 경우 기본 작업이 수행되는 경우가 있습니다.

|  | 시나리오 | 설명 | 작업 |
|---|---|---|---|
| S1 | Adobe은 일반 프로덕션 작업 중에 MVPD가 통합하는 문제를 식별합니다. | 일반적인 프로덕션 작업 중에 Adobe은 인증/인증 흐름을 수행할 수 없는 MVPD 중 하나에 대한 문제를 확인합니다(예: 만료된 인증서, 만료된 SAML 응답, 닫힌 포트, 변경된 매개 변수 등). | - Adobe은 영향을 받은 MVPD 및 프로그래머에게 알립니다.  </br> </br> - Adobe은 영향을 받는 모든 프로그래머에 대해 이 MVPD를 비활성화합니다. </br> </br> - Adobe은 MVPD와 합의된 지원 절차에 따라 MVPD와 함께 티켓을 엽니다. |
| S2 | Adobe이 프로그래머에 대해 새 MVPD를 활성화하고 프로그래머가 실행 날짜 이전에 MVPD를 허용합니다. | Adobe이 Programmer 사이트에 대해 새 MVPD를 활성화하고 있습니다. 이렇게 하지 않아도 사이트에 새 MVPD가 이미 선택기에 표시됩니다. | - Adobe은 예약된 날짜 이전에 선택기에 표시되는 새 MVPD에 대해 프로그래머에게 알립니다. </br> </br>  - 필요한 경우 프로그래머가 선택기에서 제거하는 작업을 수행합니다. |
| S3 | Adobe이 MVPD가 프로덕션 상태에 들어갈 준비가 되지 않았더라도 프로그래머에 대한 새 MVPD를 활성화합니다 | Adobe이 프로그래머에 대해 새 MVPD를 활성화하고 있지만 MVPD가 아직 통합 지원을 배포하지 않아 인증/권한 흐름을 수행할 수 없습니다 | - Adobe이 프로그래머가 요청하면 배포가 수행됩니다 </br> </br> - 프로그래머는 모든 테스트가 수행되면 MVPD의 허가를 보장할 책임이 있습니다. |

## 심각도 1 장애에 대한 응답 예상 {#response-expectations-for-severity-one-incidents}

* 초기 응답: 30분 (24/7)
* 작업 계획: 1시간 (24/7)
* 해결 방법: ASAP (24/7)

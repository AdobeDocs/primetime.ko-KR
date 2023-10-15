---
title: 동시성 모니터링 에스컬레이션 절차
description: 동시성 모니터링 에스컬레이션 절차
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# 동시성 모니터링 에스컬레이션 절차 {#esc-procedures}

>[!NOTE]
>
>핫라인 +1-205-693-9813으로 전화하여 다음으로 이메일 보내기 `tve-support@adobe.com` 제목란에 &quot;긴급 - 문제&quot;를 포함합니다.


## 소개 {#cm-escalation-intro}

이 문서에서는 주요 장애 지원 절차(**심각도 1** level) Adobe Primetime 인증, Primetime 동시 모니터링 및 해당 파트너에 영향을 미칩니다.

## 에스컬레이션 심각도 1 수준의 정의 {#defn-escl-sevrityone-level}

A **심각도 1** 수준 인시던트가 **라이브** 상황, **프로덕션 환경에서 발생**&#x200B;는 하나의 채널 및 하나의 MVPD에 대한 인증 및/또는 권한 부여 흐름의 완료를 허용하지 않으므로 흐름을 수행하는 MVPD의 많은 가입자에게 영향을 줍니다.

## 심각도 1 인시던트의 예 {#exampl-sevone-incident}

* 다음 위치에 호스팅된 프로덕션 Access Enabler <http://entitlement.auth.adobe.com/entitlement/AccessEnabler.js> 을(를) 사용할 수 없습니다.

* 특정 MVPD의 경우, Adobe은 사용자가 (지원되는 브라우저에서) MVPD를 선택한 후 더 이상 로그인 페이지를 리디렉션/표시하지 않습니다.

* 파트너는 사용자가 특정 MVPD로 인증/승인할 수 없다는 보고를 많이 받습니다.

* 인증 프로세스 중에 인증/권한 부여 플로우를 다시 시작하지 못한 채 사용자가 Adobe 오류 페이지에서 멈춥니다.


## 의 예 *아님* 심각도 1 문제 {#exampl-not-sev1}

*이러한 유형의 문제에 대해 Adobe은 조사에 대한 지원을 제공하지만 심각도 1 인시던트는 아닙니다.*

* Flash 버전 문제(Flash 누락, Flash 차단기, 잘못된 Flash 버전)로 인해 하나 또는 일부 구독자가 흐름을 수행할 수 없습니다.
* 한 명 또는 몇 명의 구독자가 인증할 수 없으며 MVPD 로그인 페이지에 남아 있습니다.
* 한 명 또는 몇 명의 구독자가 인증되었지만 비디오를 재생할 수 없습니다.
* 한 명/일부/모든 구독자에게 프로그래머 사이트에서 JavaScript 오류가 발생합니다.

## 심각도 1 에스컬레이션 흐름 {#sevone-escalation-flows}

심각도 1 인시던트는 Adobe 또는 Adobe Primetime 인증 파트너에 의해 시작될 수 있습니다. 각 단계에 대한 단계는 아래에 나와 있습니다.

### 파트너가 시작한 플로우 {#partner-initiated-flow}

1. 파트너는 위에서 설명한 대로 Adobe의 즉각적인 주의가 필요한 심각도 1 인시던트를 식별합니다.

1. 파트너는 제목란에 &quot;URGENT - INCIDENT&quot;를 포함하여 다음 정보를 추가하는 이메일을 tve-support@adobe.com에 보냅니다.

   * 제목
   * 설명 및 재현 단계
   * OS
   * 브라우저
   * Flash 버전
   * (선택 사항) 문제를 보여 주는 사용 가능한 스크린샷 또는 비디오 캡처입니다

1. Adobe이 30분 내에 티켓에 응답하지 않으면 아래 번호로 전화를 겁니다.

   * **1-205-693-9813**


**티켓 제목에 &quot;URGENT-INCIDENT&quot;를 포함하지 않으면 알림 시스템에서 선택하지 않습니다.**

### Adobe 시작 흐름 {#adobe-initiated-flow}

**...Adobe Primetime 인증 문제**

1. Adobe은 내부 문제를 식별하고 추적 시스템으로 티켓을 엽니다.

1. Adobe은 티켓 번호와 예상 문제 영향을 지정하여 파트너의 프로그램 관리자 및 기술 담당자에게 알립니다.

1. Adobe은 사고 해결을 위해 노력하며 영향을 받는 모든 파트너에게 계속 정보를 제공합니다.


**...파트너 문제(프로그래머/MVPD)**

1. Adobe은 MVPD 또는 프로그래머 사이트 중 하나와의 통합과 관련된 문제를 식별합니다.

1. Adobe이 영향을 받는 파트너에게 알림 **해당 파트너와 적절한 지원 절차 준수** 파트너의 지원 조직에 티켓을 엽니다.

1. 영향 분석 중에 Adobe이 문제가 사고 시나리오에 대해 미리 합의된 결정 중 하나에 속한다는 것을 알게 되면(아래 &quot;사고 시나리오에 대해 미리 합의된 결정&quot; 섹션 참조) partner1을 기다리지 않고 적절하게 동작합니다. 의 입력입니다.

1. Adobe은 서비스가 복원되면 파트너의 업데이트와 파트너의 알림을 기다립니다.

### 사고 시나리오에 대한 사전 동의 결정 {#pre-agreed-decisions}

해당 시나리오가 발생하는 경우 기본 작업이 수행되는 몇 가지 상황이 있습니다.

|    | 시나리오 | 설명 | 작업 |
|:---:|:---|:---|:---|
| S1 | Adobe은 정상적인 프로덕션 작업 중 MVPD의 통합 문제를 식별합니다. | 정상적인 프로덕션 작업 중에 Adobe은 인증/권한 부여 흐름을 수행할 수 없는 MVPD 중 하나의 문제를 확인합니다(예: 만료된 인증서, 만료된 SAML 응답, 닫힌 포트, 변경된 매개 변수 등). | Adobe은 영향을 받는 MVPD 및 프로그래머에게 알립니다. Adobe은 영향을 받는 모든 프로그래머에 대해 이 MVPD를 비활성화합니다. Adobe은 해당 MVPD와의 합의된 지원 절차에 따라 MVPD와의 티켓을 엽니다 |
| S2 | Adobe은 프로그래머를 위해 새 MVPD를 활성화하고 프로그래머는 출시일 전에 MVPD를 허용 목록에 추가합니다. | Adobe은 프로그래머 사이트에 대한 새 MVPD를 활성화하고 있으며 새 MVPD가 아직 표시되지 않았더라도 선택기에 이미 표시되어 있습니다. | Adobe은 예정된 날짜 이전에 선택기에 나타나는 새 MVPD에 대해 프로그래머에게 알립니다. 프로그래머는 필요한 경우 선택기에서 제거하기 위한 동작을 취하게 된다. |
| S3 | Adobe은 MVPD가 프로덕션에 들어갈 준비가 되지 않았더라도 프로그래머를 위해 새 MVPD를 활성화합니다 | Adobe이 프로그래머를 위해 새 MVPD를 활성화하고 있지만 MVPD가 아직 통합 지원을 배포하지 않아 인증/권한 부여 흐름을 수행할 수 없습니다 | Adobe은 프로그래머가 요청하는 경우에만 배포를 수행합니다. 프로그래머는 모든 테스트가 수행되면 MVPD의 허용 목록을 확인할 책임이 있습니다. |

### 심각도 1 인시던트에 대한 응답 예상 {#response-expectations}

* 초기 응답: 30분(24/7)
* 작업 계획: 1시간(24/7)
* 해결 방법: ASAP (24/7)
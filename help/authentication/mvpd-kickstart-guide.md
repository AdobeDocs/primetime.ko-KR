---
title: MVPD 직접 통합 계획
description: MVPD 직접 통합 계획
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# MVPD 킥스타트 안내서: MVPD 직접 통합 계획 {#mvpd-dir-int-plan}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#mvpd-kickstart-intro}

TV Everywhere용 Adobe Primetime 인증을 시작합니다.  당신과 함께 일하기를 기대합니다.

>[!NOTE]
>
>MVPD(Multichannel Video Programming Distribution)에 대한 킥스타트 안내서입니다. 프로그래머(콘텐츠 공급자)인 경우 [프로그래머 시작 안내서](/help/authentication/programmer-kickstart-guide.md).

Zendesk의 Primetime 인증 티켓 시스템을 통해 항상 지원이 제공됩니다. 또한 이 위치에서 프로세스에 대한 샘플, 설명서 및 비디오 자습서를 찾을 수 있습니다. 를 사용하려면 [Zendesk](https://adobeprimetime.zendesk.com/)https://tve.zendesk.com/home에서 계정을 등록하고 만들어야 합니다. 등록할 수 있는 사용자 및 제출된 티켓에 대한 댓글을 보거나 게시할 수 있는 사용자에게는 제한이 없습니다. 모든 지원 질문은 다음 주소로 해야 합니다. adobe.com에서 tve 지원

**팀 연락처**:

**지원** - 모든 질문, 사고 또는 기능 요청에 대해 **tve-support@adobe.com**.

## 1. 회의 시작 {#kickoff-meetings}

이러한 모임의 범위는 Adobe과 MVPD 간의 기술적인 토론의 시작입니다. 이 프로세스 시점에서 설명서를 양측에서 공유해야 합니다. 따라서 Adobe은 통합 상태를 추적하려면 티켓 시스템(https://tve.zendesk.com/)에서 티켓을 열어야 합니다.

## 2. 기능 {#features}

Adobe은 통합의 전체 일정, 단계, 타임라인 및 구현 세부 사항을 논의하고 추적하기 위해 주별 상태 호출을 설정합니다. 이 단계에서 Adobe은 MVPD 사양을 검토합니다. 그 결과는 MVPD에 필요한 모든 기능을 자세히 설명하는 사양 페이지여야 합니다. MVPD는 MVPD의 인증/인증 구현을 자세히 설명하는 사양 문서를 Adobe에게 보냅니다.

명확히 할 항목은 [MVPD 통합 기능](/help/authentication/mvpd-integr-features.md).

이 시점에서 자세히 설명해야 하는 몇 가지 설정이 있습니다.

* **MVPD의 로고 URL** - 다음 크기를 갖는 파일입니다. 112 x 33픽셀 사용자가 로그인 단추를 클릭하여 유료 TV 공급자를 선택하면 해당 사이트에 프로그래머가 표시됩니다.
* **TTL(time-to-live) 값** - TTL은 일반적으로 인증/인증 프로세스 중에 MVPD가 설정합니다. 그러나 Adobe은 해당 TTL 값을 재정의하고 프로그래머와 MVPD 모두에서 동의한 내용에 따라 다른 값을 제공할 수 있습니다.
* **표시 이름** - 사용자가 로그인 단추를 클릭하여 유료 TV 공급자를 선택하면 해당 사이트의 프로그래머가 표시됩니다.
* **테스트 자격 증명** - 두 프로필(스테이징 및 프로덕션)에는 테스트 자격 증명 목록이 있어야 합니다.

>[!IMPORTANT]
>
>사용자가 자격 부여 흐름을 시작할 때마다 하나의 불투명 고유 사용자 ID와 연결됩니다.  사용자 ID는 Programmer 앱의 사용자를 식별하는 데 사용되지만 MVPD에서 나옵니다.

>[!CAUTION]
>
>각 MVPD에 대한 중요 알림: 사용자 ID는 사용자를 식별, 연락 또는 찾기 위해 단독으로 사용하거나 다른 정보와 함께 사용할 수 있는 PII(개인 식별 정보)를 포함하지 않아야 합니다.

## 2. 메타데이터 교환 {#metadata-ex}

양측은 관련된 모든 환경(프로덕션, 스테이징 등)에 대한 메타데이터를 교환해야 합니다.

* **Adobe**
   * 스테이징 환경 Adobe의 SP 메타데이터는 다음 위치에서 검색할 수 있습니다. [인증 스테이징 sp 메타데이터](https://sp.auth-staging.adobe.com/sp/metadata)
   * 프로덕션 환경 Adobe의 SP 메타데이터는 다음 위치에서 검색할 수 있습니다. [인증 운영 sp 메타데이터](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * 메타데이터(스테이징/프로덕션)를 추가하려면

## 4. IP 목록 허용 {#allow-ip-list}

다음 IP는 MVPD 방화벽의 허용 목록에 포함되어야 합니다. IP 목록은 Adobe에 문의하십시오.

* Primetime 인증을 사용하려면 제한된 리소스에 액세스할 수 있도록 방화벽이 포트 80 및 443에서 열려 있어야 합니다.

* MVPD는 인증 및 인증 서버에 대한 IP 주소 목록을 추가해야 합니다(이 경우).

## 5. 개발 {#deve}

개발 단계의 기간은 세부 항목을 검토한 후, 양측이 승인하는 항목을 고려하여 결정될 것이다. Adobe은 인증 부분에 대한 사용자 지정 코드를 작성해야 합니다.

>[!NOTE]
>
>권한은 리소스별로 수행됩니다. 인증 트랜잭션은 일반적으로 사용자가 인증을 요청하는 채널을 나타내는 Programmer의 사이트에서 전달된 ID 문자열로 수행됩니다. 이 리소스 ID는 Programmer와 MVPD 사이에 설정되며 필요한 만큼 세분화할 수 있습니다.

## 6. Adobe 환경 {#adobe-env}

Adobe은 개발 프로세스의 여러 단계에 대해 다른 환경을 제공합니다.

* **사전 자격** (QUAL 전): QUAL 이전 환경에는 다음 릴리스 후보가 포함되어 있습니다. Adobe은 통합을 릴리스 환경으로 업그레이드하기 전에 처음에 이 환경에서 새 파트너를 통합합니다. 파트너는 QUAL 이전 환경에서 테스트할 2주가 있으며 PRE-QUAL 구성의 변경을 명시적으로 요청해야 합니다(변경 요청 프로세스에 대한 자세한 내용은 Adobe 담당자에게 문의). 버그 수정은 이 환경에서 새 배포를 트리거합니다.
* **릴리스** (릴리스): Adobe의 현재 프로덕션 빌드는 여기에서 라이브 환경에 배포됩니다.

Adobe 환경을 사용하는 방법에 대한 자세한 내용은 [Adobe 환경 이해](/help/authentication/understanding-the-adobe-environments.md)

## 7. 스테이징 배포 {#stag-env}

Adobe은 MVPD에서 받은 메타데이터를 기반으로 Primetime 인증 시스템에서 새로운 MVPD를 만들고 구성합니다. 이 배포는 Adobe의 사전 준비 스테이징 환경에 배포되며 테스트 프로그래머(Test배포자)로 구성됩니다.

MVPD는 QA/스테이징/테스트 환경에서 동일한 배포를 수행해야 합니다.

## 8. 테스트 및 문제 해결 {#tes-troubleshoot}

이 단계에서 Adobe 및 MVPD 테스트를 수행하고 통합 문제를 해결합니다. 통합을 테스트하는 데 도움이 되도록 Primetime 인증 팀은 Adobe의 API 테스트 사이트를 사용할 수 있습니다. Adobe의 API 테스트 사이트 사용에 대한 자세한 내용은 [Adobe API 테스트 사이트를 사용하여 인증 및 인증 흐름 테스트](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

테스트 및 문제 해결 이 성공적으로 완료되면 Adobe의 릴리스 스테이징 환경에서 통합이 활성화됩니다. 이때 Adobe은 MVPD를 실제 프로그래머와 통합할 수 있습니다.

## 9. 생산 배치 {#prod-dep}

* 연결을 테스트하려면 MVPD가 프로덕션 프로필에 먼저 배포해야 합니다.

* Adobe은 사전 프로덕션에 배포됩니다.

* 이제 모든 당사자가 프로덕션 프로필에서 테스트할 수 있습니다.

* 이 시점에서 모든 것이 정상이면 Adobe은 통합을 모든 사용자가 사용할 수 있는 릴리스 프로덕션 환경(&quot;live&quot;)으로 이동할 수 있습니다.

## 10. 에스컬레이션 절차 {#esc-proc}

통합이 프로덕션에 가동되면 최상의 고객 경험을 제공하는 것이 중요합니다. 서버 작동 중지 문제가 발생할 경우 최상의 응답을 보장하려면 MVPD가 Adobe의 주의를 끄는 문제에 대한 에스컬레이션 절차 설명서를 제공해야 합니다.

이때 Adobe은 MVPD에게 최신 Primetime 인증 에스컬레이션 프로세스를 제공합니다.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->

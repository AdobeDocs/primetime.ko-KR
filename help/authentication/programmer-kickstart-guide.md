---
title: 프로그래머 킥스타트 안내서
description: 프로그래머 킥스타트 안내서
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# 프로그래머 킥스타트 안내서 {#programmer-kickstart-guide}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#prog-kickstart-guide-intro}

TV Everywhere용 Adobe Primetime 인증을 시작합니다. 당신과 함께 일하기를 기대합니다.

>[!NOTE]
>
>프로그래머(컨텐츠 공급자)를 위한 Kickstart 안내서입니다. MVPD(Multi-Channel Video Programming Distributor)를 사용 중이라면 다음을 확인하십시오. [MVPD 시작 안내서](/help/authentication/mvpd-kickstart-guide.md).


Adobe Primetime 인증 연락처:

* 지원 - 모든 질문, 사고 또는 기능 요청에 대해, `tve-support@adobe.com`
* 프로젝트 시작 시기까지 지원 연락처가 프로젝트에 지정됩니다.

다음 정보에서는 강력하고 효율적인 시작을 위한 몇 가지 중요한 첫 번째 단계를 간략하게 설명합니다. 목표는 통합을 위해 파트너와 협력하는 방법에 대한 설명과 기대를 제공하는 것입니다. 각 항목에 대해 아래의 &quot;제공&quot; / &quot;Adobe에서 제공&quot; 섹션을 참조하십시오. 이러한 목록은 프로젝트 작업 시 검사 목록 또는 가이드를 통해 표시됩니다.

이 문서에서는 프로그래머가 선택한 MVPD 파트너와 함께 작업하도록 등록되어 있다고 가정합니다.

## 릴리스 일정 {#release-schedule}

Adobe Sprint 개발 주기는 릴리스가 예약되는 시점과 각 릴리스가 개발 시스템을 통해 승격되는 방법을 볼 수 있도록 계획되어 있습니다.

각 스프린트가 완료되면 QE에 사용하거나 UAT 서버에서 새로운 구현을 볼 수 있습니다.

대략 6주마다 Adobe 사전 자격 서버에 릴리스가 제공됩니다. (최종 QE를 수행하는 동안 제안된 다음 릴리스를 보류하는 서버입니다.) 이러한 빌드에는 마지막 감소 이후 스프링트에서 완료된 모든 작업이 포함됩니다. 파트너가 이 릴리스를 테스트할 수 있도록 현재 2주 QE 기간 을 사용할 수 있습니다.

이전 2주 테스트 기간 동안 중요한 문제가 발생하지 않았다고 가정하면 릴리스가 라이브 프로덕션으로 승격됩니다. 즉, 통합은 Adobe 릴리스 환경에서 사용할 수 있지만 파트너는 릴리스 정보를 공개할 때 선택합니다.

<!--For the latest release schedule information, see the Release Calendar.-->

## 지원 설명서 {#supp-doc}

Adobe은 다음을 제공합니다.

* 배포 안내서: **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* Zendesk 고객 지원 시스템에 액세스합니다. 또한 일부 프로세스에 대한 샘플, 정보 및 비디오 자습서를 찾을 수 있습니다. Zendesk에서 이 문서에 액세스하려면 Zendesk에 게시된 다른 문서와 함께 계정을 등록하고 만들어야 합니다. `https://tve.zendesk.com/home`. 등록할 수 있는 사용자 수에는 제한이 없습니다.  제출된 티켓에 대한 의견을 보고 공유할 수 있습니다. 모든 지원 질문은 `tve-support@adobe.com`.
* [Programmer Integration 안내서](/help/authentication/programmer-integration-guide-overview.md)
* 미디어 토큰 확인자 라이브러리: `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## 테스트 환경 설정 {#test-env-setup}

Adobe이 먼저 Adobe 테스트 사이트를 설정합니다. 이 사이트에서는 Adobe이 테스트 목적으로 MVPD 역할을 합니다. 그런 다음 팀이 Adobe API를 호출하는 테스트 웹 사이트를 설정할 수 있습니다. 기본 MVPD 선택기를 사용하고 idP로 &quot;Adobe&quot;을 선택합니다.

다음을 제공합니다.

1. 요청자 ID. 이 문자열은 웹 사이트 또는 Adobe Primetime 인증을 요청하는 애플리케이션의 브랜드를 고유하게 식별하는 문자열입니다. 문자열 자체는 임의적이지만 Adobe과 프로그래머 간에 동의해야 합니다
1. 채널 정보. 요청자 ID에서 요청하는 콘텐츠 채널을 식별하는 문자열 세트입니다. 대부분의 경우 채널과 요청자 ID가 동일합니다. 그러나 동일한 ID로 요청할 수 있는 여러 채널의 컨텐츠가 있을 수 있습니다. 채널 이름 문자열은 케이블 TV 채널에 해당해야 합니다. 일부 MVPD는 AuthN 및/또는 AuthZ 프로토콜을 통해 이 값의 유효성을 검사합니다.
1. 도메인 이름(해당 요청자 ID에 대해 허용됨). 요청자 ID를 수락하기 위해 Adobe이 나열하는 실제 도메인 이름 목록입니다. 이렇게 하면 승인된 도메인만 메타데이터로 Adobe Primetime 인증에 액세스할 수 있습니다. 참고: 프로덕션에 유효한 도메인 이름은 테스트/스테이징에 대해 다를 수 있으며, 둘 다 제공하고 식별해야 합니다.

Adobe이 계정을 설정하고 Adobe이 다음을 제공합니다.

* 테스트 사이트에 액세스하기 위한 로그인 및 암호

## MVPD를 사용하여 설정 {#setup-mvpd}

이 섹션에서는 Adobe 테스트 사이트에서 MVPD와 함께 작동하도록 마이그레이션할 때 필요한 사항을 설명합니다.

MVPD를 통해 다음을 제공합니다.

* **자격 증명 세트 2개**:
   * AuthN + AuthZ : 인증 및 인증된 사용자의 로그인/암호
   * AuthN + Non-AuthZ : 인증되었지만 인증되지 않은 사용자의 로그인/암호
* **리소스 ID**. AuthZ 프로토콜을 통해 MVPD와 함께 유효성 검사되는 특정 콘텐츠 식별자입니다. 채널, 표시, 에피소드 또는 자산 수준에서 지정할 수 있습니다. MVPD와 동의해야 합니다.

Adobe Primetime 인증은 MRSS 기반 메타데이터 스키마를 지원하며, 이는 리소스 ID가 필요한 만큼 구체적일 수 있고, 특정 MVPD에 고유한 식별자를 포함할 수 있음을 의미합니다.

**새로운 MVPD 통합**: 선택한 MVPD가 통합을 완료하는 데 필수적인 부분을 재생한다는 것을 기억해야 합니다. Adobe은 각 MVPD의 스펙에 따라 코드를 작성해야 합니다. 이 단계가 완료되기 전까지는 대화 상자에서 해당 MVPD를 선택하거나 제품 테스트를 완료할 수 없습니다. Adobe은 다음 사용 가능한 스프린트에 맞게 이 작업을 미리 예약해야 합니다. (현재 스케줄 정보에 대해서는 릴리즈 달력을 참조하십시오.)

**기존 MVPD 통합**: 선택한 MVPD가 이미 Adobe을 사용하여 설정된 경우 연결 단계가 훨씬 간단해야 합니다(더 빠름). 종종 구성 변경 방식으로 연결을 구현할 수 있습니다.

>[!NOTE]
>
>MVPD는 여전히 프로그래머를 활성화하고 관련 사업 거래에 서명해야 할 것이다.

**MVPD가 있는 QE**: 모든 통합에는 공동 QE가 포함되며, 최종 사용자가 궁극적으로 MVPD의 고객이므로 많은 고객들이 &quot;라이브&quot;를 푸시하기 전에 테스트 주기를 설정했습니다. 이 작업에는 MVPD 리소스 예약이 포함되므로 이 작업은 지연될 가능성이 있습니다.

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->


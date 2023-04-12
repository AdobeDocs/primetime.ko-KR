---
title: Primetime TVE 대시보드 사용 안내서
description: Primetime TVE 대시보드 사용 안내서
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4386'
ht-degree: 0%

---


# Primetime TVE 대시보드 사용 안내서 {#tve-db-user-guide}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#tve-db-intro}

[[!DNL Adobe] TVE 대시보드(TVE 대시보드)](https://console.auth.adobe.com/) 는 Adobe Primetime 인증 제품 팀과 비즈니스 관계가 있는 미디어 회사(프로그래머)에서 일하는 사용자를 위한 셀프 서비스 대시보드입니다.

액세스 권한을 얻으려면 기술 계정 관리자(TAM)에게 문의하십시오. 액세스 권한을 얻으려면 Adobe Marketing Cloud 조직에 두 개의 새 사용자 그룹을 구성해야 합니다.

* TVE 대시보드 읽기-쓰기 - 이 그룹의 구성원은 대시보드의 편집 가능한 모든 섹션에 전체 권한을 갖습니다
* TVE 대시보드 읽기 전용 - 이 그룹의 구성원은 전체 대시보드에 대한 보기 권한만 갖습니다


이 사용 안내서를 자세히 살펴보려면 다음 리소스를 참고하여 Adobe Primetime 인증 제품 팀에서 제공하는 흐름 및 기능을 잘 이해하고 본 문서에서 사용하는 용어를 숙지해야 합니다.

* [TVE 기술 문서](/help/authentication/technical-paper.md)
* [Programmer Kickstart 안내서](/help/authentication/programmer-kickstart-guide.md)
* [자격 흐름](/help/authentication/entitlement-flow.md)
* [용어 설명](/help/authentication/glossary.md)


이 사용 안내서의 다음 섹션을 계속 진행하면 회사의 채널, 프로그래머 또는 채널과 MVPD(Multichannel Video Program Distributor) 간의 통합에 대해 다양한 설정을 관리하는 방법을 알아봅니다.

>[!IMPORTANT]
>TVE 대시보드 는 기본 및 고급 작업 공간 간에 전환하는 옵션을 제공합니다. 오른쪽 상단 모서리의 아이콘을 전환하여 이 작업을 수행할 수 있습니다. Advanced Workspace는 Adobe Primetime 인증 제품 팀에서 제공하는 기능에 대한 고급 지식뿐만 아니라 기술적인 지식이 있는 사용자를 대상으로 합니다.

![TVE 대시보드 작업 공간](assets/tve-basic-advanced-workspace.png)

*그림 1: Adobe Primetime TVE 대시보드 &quot;기본/고급 작업 공간&quot; 드롭다운*

## 환경 {#authn-environments}

사용자가 수행해야 할 작업에 따라 Adobe Primetime 인증 환경 간을 전환해야 할 수 있습니다. Adobe Primetime 인증 환경에 대한 자세한 내용은 다음 문서를 참조하십시오. [Adobe Primetime 인증 환경 이해](/help/authentication/understanding-the-adobe-environments.md).

TVE Dashboard는 아래와 같이 Prequaly(Prequalification)와 Release라는 두 개의 환경을 제공하며, 각각 스테이징과 프로덕션이라는 두 개의 프로필이 있습니다.

* [사전 준비 스테이징](https://console-prequal.auth-staging.adobe.com/)
* [사전 프로덕션](https://console-prequal.auth.adobe.com/)
* [릴리스 스테이징](https://console.auth-staging.adobe.com/)
* [릴리스 프로덕션](https://console.auth.adobe.com/)

환경 간을 전환하려면 아래 표시된 드롭다운 요소에서 항목으로 표시되는 원하는 환경을 클릭하면 됩니다.

![TVE 대시보드 환경 드롭다운](assets/tve-dashboard-env.png)

*그림 2: Adobe Primetime TVE 대시보드 환경 드롭다운*

>[!IMPORTANT]
>TVE Dashboard를 통해 Adobe Primetime 인증 구성을 관리 변경할 때 적절한 기능을 보장하려면 아래 시퀀스를 따르는 것이 좋습니다.

TVE 대시보드를 통해 Adobe Primetime 인증 구성을 관리 변경하려면:

* 에서 변경 작업을 수행합니다. [스테이징을 해제하고 유효성을 확인합니다](http://sp.auth-staging.adobe.com/apitest/api.html).
* 에서 변경 작업을 수행합니다. [사전 프로덕션 및 유효성 검사](http://sp.auth-staging.adobe.com/apitest/api.html).
* 에서 변경 작업을 수행합니다. [프로덕션 릴리스 및 유효성 검사](http://sp.auth-staging.adobe.com/apitest/api.html).

>[!IMPORTANT]
>관리 변경 사항이 라이브로 전환되도록 하려면 사용자가 사이드바의 왼쪽 하단에 표시되는 버튼을 선택하여 &quot;검토 및 푸시 변경 사항&quot; 섹션으로 이동하여 변경 사항을 검토하려면 새로 만든 변경 사항에 대한 설명을 추가하고 &quot;푸시 구성&quot;을 선택하여 구성 업데이트를 확인해야 합니다.

![대시보드 검토 및 푸시 알림](assets/tve-review-push-notifications.png)

*그림 3: Adobe Primetime TVE 대시보드 검토 및 푸시 변경 알림*

## 섹션 {#sections}

미디어 회사(프로그래머)에서 일하는 사용자는 사이드바에서 TVE 대시보드의 다음 섹션에 액세스할 수 있습니다.

* **채널** - 콘텐츠 공급자와 관련된 설정을 포함합니다.
* **프로그래머** - 하나 또는 여러 개를 집계하는 상위 조직과 관련된 설정을 포함합니다 **채널**
* **통합** - 간의 통합과 관련된 설정을 포함합니다. **채널** 및 **MVPD**
* **MVPD** - 사용 가능한 설정과 관련된 설정을 포함합니다. **MVPD**
* **보고서** - 세 가지 유형의 보고서에 대해 집계된 데이터를 포함합니다. AuthN TTL, AuthZ TTL, SSO
* **변경 로그** - TVE 대시보드 구성에 적용된 최신 수정 사항을 포함합니다

![TVE 대시보드 섹션](assets/tve-dashboard-sections.png)

*그림 4: Adobe Primetime TVE 대시보드 섹션*

### 채널 {#tve-db-channels-section}

이 섹션에서는 사용 가능한 채널에 대한 설정을 보고 편집하거나 새 채널을 만들 수 있습니다. 사용 가능한 채널 중 하나를 클릭하면 다음 탭이 있는 화면이 표시됩니다.

* **채널 데이터**
   * **채널 Id** - Adobe 시스템에 사용되는 채널의 고유 ID를 &quot;요청자 ID&quot;라고도 합니다.
   * **표시 이름** - 채널의 상업적 이름.
* **일반 설정**
   * **Analytics 구성** - Adobe Analytics에 전달할 Adobe Primetime 인증 이벤트를 구성합니다. 이 기능을 활성화하기 전에 RSID(보고서 세트 ID)를 구성하는 방법에 대한 자세한 내용은 Adobe에 문의하십시오.
* **인증서**

   발급 조직, 발행 날짜 및 만료 날짜와 함께 인증 흐름에 사용되는 인증서 목록을 포함합니다. 이러한 인증서는 개인/공개 키 역할을 하며 유효성 검사 목적으로 사용됩니다.
* **도메인**

   각 채널이 Adobe Primetime 인증과 통신할 도메인 목록을 포함합니다.
* **통합**

   사용 가능한 MVPD와의 통합 목록과 함께 활성화되거나 설정되지 않을 수 있는 각 통합 상태를 포함합니다. 통합 페이지로 이동하는 방법은 특정 항목을 클릭하면 됩니다.
* **등록된 응용 프로그램**

   애플리케이션 등록 목록을 포함합니다. 자세한 내용은 문서를 참조하십시오 [동적 클라이언트 등록 관리](/help/authentication/dynamic-client-registration-management.md).

* **사용자 지정 구성표**

   사용자 지정 구성표 목록을 포함합니다. 자세한 내용은 [iOS/tvOS 애플리케이션 등록](/help/authentication/iostvos-application-registration.md) 및 [동적 클라이언트 등록 관리](/help/authentication/dynamic-client-registration-management.md)


#### 도메인 추가/삭제 {#add-delete-domains}

선택한 채널에 대해 새 도메인을 추가하는 프로세스를 시작하려면 도메인 목록 아래의 &quot;새 도메인 추가&quot; 단추를 클릭해야 합니다. 도메인 이름을 지정할 수 있는 새 도메인 항목이 만들어집니다. 도메인 목록에 더 일반적인 도메인이 이미 있으면 새 하위 도메인을 추가할 수 없습니다.

![선택한 채널 섹션에 새 도메인 추가](assets/add-domain-to-channel-sec.png)

*그림: 채널의 도메인 탭*

### 프로그래머 {#tve-db-programmers-section}

이 섹션에서는 사용 가능한 프로그래머의 설정을 보고 편집하거나 새 프로그램을 만들 수 있습니다. 사용 가능한 프로그래머 중 하나를 클릭하면 다음 탭이 있는 화면이 반환됩니다.

* **프로그래머 데이터**
   * **프로그래머 Id** - Programmer의 시스템에서 사용되는 고유 ID입니다.
   * **표시 이름** 프로그래머의 상업성
   * **로고 Url** - Programmer의 상용 로고 URL(Uniform Resource Locator)입니다.
   * **로고 미리 보기** - 위의 URL(Uniform Resource Locator)에서 다운로드하여 프로그래머의 상업용 로고 미리 보기입니다.

* **인증서**

   발급 조직, 발행 날짜 및 만료 날짜와 함께 인증 흐름에 사용되는 인증서 목록을 포함합니다. 이러한 인증서는 개인/공개 키 역할을 하며 유효성 검사 목적으로 사용됩니다.

* **채널**

   이 특정 프로그래머에 속하는 채널 목록을 포함합니다. 채널 섹션으로 이동 하려면 특정 항목을 클릭하면 됩니다.

* **등록된 응용 프로그램**

   애플리케이션 등록 목록을 포함합니다. 자세한 내용은 [동적 클라이언트 등록 관리](/help/authentication/dynamic-client-registration-management.md).

* **사용자 지정 구성표**

   사용자 지정 구성표 목록을 포함합니다. 자세한 내용은 [iOS/tvOS 애플리케이션 등록](/help/authentication/iostvos-application-registration.md) 및 [동적 클라이언트 등록 관리](/help/authentication/dynamic-client-registration-management.md).


### 통합 {#tve-db-integrations-sec}

이 섹션에서는 채널과 사용 가능한 MVPD 간의 통합에 대한 설정을 보고 편집하거나 새 설정을 만들 수 있습니다. 사용 가능한 통합 중 하나를 클릭하면 기본 작업 공간을 사용할 때 단일 페이지 또는 고급 작업 공간을 사용할 때 다음 탭이 있는 화면이 반환됩니다.

* **통합 데이터**
   * **통합 Id**- MVPD가 &quot;_&quot; 문자로 구분되는 채널의 고유 ID에 추가된 결과입니다.
   * **채널 표시 이름** - 채널의 상업적 이름.
   * **채널 Id** - Adobe 시스템에 사용되는 채널의 고유 ID를 &quot;요청자 ID&quot;라고도 합니다.
   * **MVPD 표시 이름** - MVPD의 상업명
   * **MVPD Id** - 시스템에 사용된 MVPD의 고유 ID입니다.
* **일반 설정**
   * **사용자 메타데이터 키** - 특정 통합에 사용할 수 있는 메타데이터 키를 구성합니다.
   * **플랫폼 특정 설정** - 특정 플랫폼(예: TTL, SSO 및 IFrames)에 대해 다른 설정을 구성합니다.

* **인증 설정**
   * Adobe Primetime 인증 기능과 관련된 설정을 포함합니다.
* **인증 설정**
   * Adobe Primetime 인증 권한 부여 기능과 관련된 설정을 포함합니다.
* **로그아웃 설정**
   * Adobe Primetime 인증 로그아웃 기능과 관련된 설정을 포함합니다.

#### 통합 만들기 {#create-integration}

새 통합을 만들려면 아래 단계를 수행하십시오.

* 새 통합 추가 단추를 클릭합니다.
* 채널 검색 및 선택
* MVPD 검색 및 선택
* TVE 대시보드가 &quot;통합 ID&quot;를 계산하고 사용 가능한 MVPD 끝점을 표시할 때까지 기다립니다.
* 인증, 권한 부여 및 로그아웃 끝점을 선택하거나 기본값을 사용합니다
* 통합 만들기 단추를 클릭합니다.
* MVPD 설정에 따라 팝업이 나타날 수 있고 MVPD에서 미리 제공해야 하는 추가 속성을 요청할 수 있습니다. 그렇지 않으면 새로 만든 통합 페이지로 리디렉션됩니다

![](assets/new-integration-window.png)



*그림 5. Adobe Primetime TVE Dashboard 새 통합 창*


#### 통합 업데이트 {#update-integration}

기존 통합을 업데이트하려면 통합 섹션이나 통합 탭이 있는 채널 섹션에서 해당 특정 통합에 대한 테이블 항목을 클릭하십시오.

기본 작업 공간 모드를 사용할 때 이 섹션에서는 iFrame 설정과 인증 및 인증 토큰 TTL(time-to-live) 등 가장 일반적으로 업데이트된 설정을 보고 편집할 수 있습니다. 동적으로 정의된 토큰 지속성 TTL을 지원하는 MVPD와의 통합에 대해 TTL 설정을 누락할 수 있습니다(다음 항목 1.19 참조: [MVPD 통합 요구 사항](/help/authentication/mvpd-integr-features.md)).



고급 작업 공간 모드를 사용할 때 이 섹션에서는 덜 일반적인 설정을 보고 편집할 수 있습니다.



기본 및 고급 작업 공간 모드 모두의 경우 이러한 설정을 플랫폼 수준에서 변경할 수 있습니다(예: Android에서 인증 TTL 토큰에 대한 사용자 지정 값 선택, 기본적으로 다른 모든 플랫폼).



>[!IMPORTANT]
>설정 상속 체인을 이해하는 것이 중요합니다. MVPD -> MVPD 끝점 -> 통합 -> 플랫폼. 여기서 Platform은 가장 구체적인 값을 가지며, MVPD가 가장 일반적인 기본값입니다.

![](assets/inheritance-chain-component.png)


*그림 6. Adobe Primetime TVE 대시보드 속성 상속 체인 구성 요소*


#### 플랫폼 특정 설정 {#platform-sp-settings}

이 하위 섹션을 사용하여 특정 플랫폼에 대한 설정을 재정의할 수 있습니다. 사용 가능한 플랫폼은 다음과 같습니다.

* **모든 플랫폼** - 특정 플랫폼에 대해 설정된 다른 값이 없는 경우 Programmer 구현과 관계없이 모든 플랫폼에 적용할 값을 설정합니다.
* **Android** - Adobe Primetime Authentication Android SDK를 통해 Programmer 구현에 적용할 값을 설정합니다.
* **Clientless REST API** - Adobe Primetime 인증 REST API를 통해 Programmer 구현에 적용할 값을 설정합니다.
* **Fire TV** - Adobe Primetime Authentication FireTV SDK를 통해 Programmer 구현에 적용할 값을 설정합니다.
* **Flash SDK** - 이 플랫폼은 더 이상 사용되지 않습니다. **사용되지 않음**
* **JavaScript SDK** - Adobe Primetime 인증 JavaScript SDK를 통해 Programmer 구현에 적용할 값을 설정합니다.
* **Roku** - Adobe Primetime 인증 REST API를 통해 Programmer 구현에 적용되며 &quot;Roku&quot;를 장치 유형으로 전송하는 값을 설정합니다. 이는 Roku 장치의 경우 Clientless REST API 플랫폼에 대해 설정된 값보다 우선합니다.
* **Xbox 기본 SDK** - 이 플랫폼은 더 이상 사용되지 않습니다. **사용되지 않음**
* **Xbox 360 REST API** - Adobe Primetime 인증 REST API를 통해 Programmer 구현에 적용되며 &quot;xbox&quot;를 장치 유형으로 전송하는 값을 설정합니다. 이는 Xbox 360 장치의 경우 Clientless REST API 플랫폼에 설정된 값보다 우선합니다.
* **Xbox One REST API** - Adobe Primetime 인증 REST API를 통해 Programmer 구현에 적용할 값을 설정하고 &quot;xboxOne&quot;을 장치 유형으로 보냅니다. 이는 XboxOne 장치의 경우 Clientless REST Api 플랫폼에 설정된 값보다 우선합니다.
* **iOS** - Adobe Primetime Authentication iOS SDK를 통해 Programmer 구현에 적용할 값을 설정합니다.
* **tvOS** - Adobe Primetime Authentication tvOS SDK를 통해 Programmer 구현에 적용할 값을 설정합니다.


![](assets/platform-sp-settings.png)

*그림 7. Adobe Primetime TVE 대시보드 플랫폼별 설정*


#### 플랫폼 단일 사인온 활성화 {#enable-platform-sso}

특정 통합 및 플랫폼에 대해 단일 사인온을 활성화/비활성화하려면 아래 절차를 따르십시오.

* 고급 작업 공간 모드를 사용하고 있는지 확인합니다.
* 원하는 통합으로 이동합니다
* 로 이동합니다. **일반 설정** 탭
* 단일 사인온을 활성화하거나 비활성화할 플랫폼을 선택합니다
* 전환 **단일 사인온 활성화** 원하는 값에 플래그 지정(예 / 아니오)

   >[!IMPORTANT]
   >중요한 것은 **단일 사인온 활성화** 플래그는 iOS, tvOS, Roku 및 FireTV 플랫폼에서만 사용할 수 있으며, 이러한 플랫폼에 대해 단일 사인온을 지원하는 MVPD와의 통합에만 사용할 수 있습니다.

* 전환 **플랫폼 권한 적용** 원하는 값에 플래그 지정(예 / 아니오)

   >[!IMPORTANT]
   >중요한 것은 **플랫폼 권한 적용** 플래그는 사용자의 TV Provider 구독에 대한 플랫폼 액세스 허용 또는 거부 결정을 적용할지 여부를 제어합니다. 다음 경우에 시나리오 고려 **단일 사인온 활성화** 플래그가 &quot;예&quot;로 설정되어 있습니다. **플랫폼 권한 적용** 플래그는 또한 &quot;예&quot;로 설정되고 사용자가 자신의 TV Provider 구독에 대한 플랫폼 액세스를 거부하도록 선택하면 각 애플리케이션(채널)에서 다른 애플리케이션(채널)에서 획득한 Adobe Primetime 인증 토큰을 사용할 수 없습니다.


#### 홈 기반 인증 사용 {#enable-hba}

다음에 대한 홈 기반 인증을 활성화/비활성화하려면 아래 단계를 따르십시오 **OAuth2** 기반 MVPD:

* 고급 작업 공간 모드를 사용하고 있는지 확인합니다.
* 원하는 통합으로 이동합니다
* 이동 **인증 설정** 탭
* 이동 **AuthN 동적 규칙** 하위 탭
* 전환 **HBA 시도** 원하는 값에 플래그 지정(예 / 아니오)


>[!IMPORTANT]
>&quot;HBA AuthN TTL&quot; 값을 재정의할 수 없습니다. 그렇지 않으면 인증 흐름이 예기치 않게 실패할 수 있습니다.

에 연결 **tve-support@adobe.com** saml 기반 MVPD에 대한 홈 기반 인증 활성화에 대한 정보.

### MVPD {#tve-db-mvpds-sec}

이 섹션에서는 사용 가능한 MVPD에 대한 설정을 볼 수 있습니다. 사용 가능한 MVPD 중 하나를 클릭하면 다음 탭이 있는 화면이 표시됩니다.

* **MVPD 데이터**
   * **MVPD Id** - 시스템에 사용된 MVPD의 고유 ID입니다.
   * **표시 이름** - 사용자 선택기에서 사용할 수 있는 MVPD의 상용 이름입니다.
   * **로고 Url** - MVPD의 상용 로고 URL(Uniform Resource Locator)입니다.
   * **로고 미리 보기** - 위의 URL(Uniform Resource Locator)에서 MVPD의 상업용 로고 미리 보기를 다운로드하여 표시합니다.
* **일반 설정**
   * **사용자 메타데이터 키**
      * 특정 MVPD에 사용할 수 있는 메타데이터 키.
   * **클라이언트 데이터 속성**
      * **인증 / 누적** - &quot;Yes&quot;로 설정하면 사용자가 액세스하려는 각 새 채널에 대해 새 인증 토큰이 필요합니다.
      * **수동 AuthN 사용** - Auth / Aggregator 플래그가 &quot;Yes&quot;로 설정되어 있고 Passive AuthN Enabled가 &quot;Yes&quot;로 설정된 경우 전체 브라우저 리디렉션을 설정하고 선택기를 표시하지 않고 백그라운드에서 다른 채널의 인증 프로세스가 발생합니다.
      * **인증/브라우저 세션** - &quot;예&quot;로 설정하면 브라우저를 닫은 후 로그아웃됩니다. &quot;아니요&quot;로 설정하면 사용자가 브라우저를 다시 시작하고 로그인된 상태로 유지할 수 있습니다.
      * **필요한 경우 이름** - &quot;예&quot;로 설정하면 MVPD 로그인 창에 iFrame이 필요함을 나타냅니다. iFrame 너비 및 iFrame 높이 필드는 MVPD 로그인 페이지를 로드하는 데 필요한 크기를 나타냅니다.
* **인증 설정**
   * **끝점 선택**
      * 이 필드는 MVPD에 의해 노출된 인증 끝점을 나타냅니다. 엔드포인트는 사용된 인증 프로토콜에 따라 다를 수 있습니다.
   * **AuthN 일반 설정**
      * 이 하위 탭에는 MVPD에서 사용하는 인증 프로토콜과 프로토콜 관련 정보가 표시됩니다.
   * **AuthN 인증서**
      * 이 하위 탭에는 MVPD가 인증 플로우에서 발행자 조직, 발행 날짜 및 만료 날짜와 함께 사용하는 인증서가 표시됩니다. 이러한 인증서는 개인/공개 키로 사용되며 유효성 검사 목적으로 사용됩니다.
   * **AuthN 동적 규칙**
      * 이 하위 탭에는 인증 프로세스에 적용되는 규칙이 표시됩니다. 다이어그램의 Request / Response / Token 을 누르면 인증 흐름의 해당 부분에 적용된 매개 변수가 강조 표시된 것으로 볼 수 있습니다.
* **인증 설정**
   * **끝점 선택**
      * 이 필드는 MVPD에 의해 노출된 인증 끝점을 나타냅니다. 끝점은 사용된 인증 프로토콜에 따라 다를 수 있습니다. 사용 가능한 인증 프로토콜은 SOAP, REST(클라이언트 없는 장치의 경우), SAML, XACML 및 OAUTH입니다.
   * **AuthZ 일반 설정**
      * 이 하위 탭에는 MVPD에서 사용하는 인증 프로토콜 및 프로토콜 관련 정보가 표시됩니다.
      * **프리플라이트 구성**
         * MVPD가 한 번의 호출로 사전 승인할 수 있는 리소스 수, 사용된 PreFlight 모델 및 시간 초과 임계값을 설명합니다. 특정 통합에 대해 리소스 수가 다를 수 있는 경우가 있습니다. 이를 관리하려면 &quot;**최대 프리플라이트 리소스 수**&quot;속성, 일반 설정 탭에서 사용할 수 있습니다. 이 속성은 지정된 통합에만 사용할 수 있으며 설정된 경우에만 인증 설정 -> PreFlight 구성 -> PreFlight 최대 리소스에 정의된 값 대신 사용됩니다.
      * **DOS 보호**
         * MVPD 인증 끝점에 대한 서비스 거부 보호에 대해 설명합니다. 각 필드에 대한 정확한 설명을 보려면 DOS 보호 필드 위로 마우스를 가져간 후 도구 설명을 확인하십시오.
      * MVPD가 **TempPass**, 그런 다음 **AuthZ 일반 설정** 또한 TempPass 기간에 대한 정보도 포함되어 있습니다.
      * MVPD가 **FlexibleTempPass**, 그런 다음 **AuthZ 일반 설정** 또한 TempPass 기간, 최대 리소스 수 및 식별 필드에 대한 정보도 포함되어 있습니다(아래 이미지 참조).
   * **AuthZ 인증서**
      * 이 하위 탭에는 MVPD가 인증 플로우에서 발행자 조직, 발행 날짜 및 만료 날짜와 함께 사용하는 인증서가 표시됩니다. 이러한 인증서는 개인/공개 키로 사용되며 유효성 검사 목적으로 사용됩니다.
   * **AuthZ 동적 규칙**
      * 이 하위 탭에는 인증 프로세스에 적용되는 규칙이 표시됩니다. 다이어그램의 **요청 / 응답 / 토큰**&#x200B;을 강조 표시된 대로 인증 흐름의 해당 부분에 적용된 매개 변수를 볼 수 있습니다.
* **로그아웃 설정**
   * **끝점 선택**
      * 이 필드는 MVPD에 의해 노출된 로그아웃 끝점을 나타냅니다. 제공된 프로토콜은 SAML 또는 OAuth2일 수 있습니다.
      * **로그아웃 일반 설정**
         * 이 하위 탭에는 MVPD에서 사용하는 로그아웃 프로토콜 및 프로토콜 관련 정보가 표시됩니다.
         * **로그아웃 응답 필요 서명** - &quot;Yes&quot;로 설정하면 신뢰할 수 있는 인증서로 응답을 서명해야 합니다.
      * **인증서 로그아웃**
         * 이 하위 탭에는 MVPD가 발급자 조직, 발행 날짜 및 만료 날짜와 함께 로그아웃 플로우에서 사용하는 인증서가 표시됩니다. 이러한 인증서는 개인/공개 키로 사용되며 유효성 검사 목적으로 사용됩니다.
      * **동적 규칙 로그아웃**
         * 이 하위 탭에는 로그아웃 프로세스에 적용되는 규칙이 표시됩니다. 다이어그램의 **요청 / 응답 / 토큰**&#x200B;을 강조 표시된 대로 로그아웃 흐름의 해당 부분에 적용된 매개 변수를 확인할 수 있습니다.

### 보고서 {#tve-db-reports-sec}

이 섹션으로 이동하려면 &quot;[대시보드 섹션](#sections)&quot; 메뉴 아래의 제품에서 사용할 수 있습니다. 이렇게 하면 3개의 탭이 있는 화면으로 이동합니다. 이 화면은 다음 하위 섹션에 자세히 표시됩니다. [AuthN TTL 보고서](#authn-ttl-reports), [AuthZ TTL 보고서](#authz-ttl-reports), [SSO 보고서](#sso-reports).

이 섹션에서는 모든 플랫폼에서 다양한 MVPD와 함께 채널/s 통합을 위해 여러 유형의 보고서에 대해 집계된 데이터를 보고 내보낼 수 있습니다.

#### 플랫폼 {#report-platforms}

모든 보고서는 다음 플랫폼에서 값을 집계합니다.

**브라우저**
Adobe Primetime 인증 JavaScript SDK를 통해 프로그래머 구현에 적용할 값을 표시합니다.

**모바일: iOS**
Adobe Primetime Authentication iOS SDK를 통해 Programmer 구현에 적용할 값을 표시합니다.

**모바일: ANDROID**
Adobe Primetime Authentication Android SDK를 통해 Programmer 구현에 적용할 값을 표시합니다.

**모바일: 기타**
모바일 장치용으로 개발된 Adobe Primetime 인증 REST API를 통해 Programmer 구현에 적용할 값을 표시합니다.

**TVCD: ROKU**
Adobe Primetime 인증 REST API를 통해 Programmer 구현에 적용되며 &quot;Roku&quot;를 장치 유형으로 전송하는 값을 표시합니다.

**TVCD: FIRETV**
Adobe Primetime Authentication FireTV SDK를 통해 Programmer 구현에 적용할 값을 표시합니다.

**TVCD: APPLETV**
Adobe Primetime Authentication tvOS SDK를 통해 Programmer 구현에 적용할 값을 표시합니다.

**TVCD: 기타**
TV 연결 장치용으로 개발된 Adobe Primetime 인증 REST API를 통해 Programmer 구현에 적용할 값을 표시합니다.

**플랫폼: UKNOWN**
Adobe Primetime 인증 서비스가 알 수 없는 장치 유형을 감지하는 Programmer 구현에 적용할 값을 표시합니다.

의 메커니즘 검토 [클라이언트 정보 전달](/help/authentication/passing-client-information-device-connection-and-application.md) 원하는 장치 유형을 전송하는 방법에 대한 자세한 내용은 Adobe Primetime 인증 REST API 또는 SDK에 문의하십시오(예: &quot;Roku&quot;).

모든 보고서는 각 Adobe Primetime 인증 환경에 고유한 구성을 기반으로 계산된 값을 집계합니다. 따라서 서로 다른 TVE 대시보드 환경 간을 전환할 때 다른 보고 데이터를 예상할 수 있습니다.

다음 문서를 검토하십시오 [환경](#authn-environments) 섹션을 참조하십시오.


##### 특정 채널/MVPD 선택 {#selecting-specific-channels-mvpds}

모든 보고서를 사용하면 특정 채널을 선택하거나 결과 보고서에 포함할 특정 MVPD를 선택하여 필터를 사용할 수 있습니다.

하나 이상의 채널을 선택하려면 **드롭다운 목록** &quot;보고서에 대해 선택한 채널&quot; 레이블 뒤에 배치됩니다. 그림 8 을 참조하십시오./9./10. 이미지 가져오기.

하나 이상의 MVPD를 선택하려면 **드롭다운 목록** &quot;보고서에 대해 선택된 MVPD&quot; 레이블 다음에 배치됩니다. 그림 8 을 참조하십시오./9./10. 이미지 가져오기.

기본적으로 데이터는 모든 회사의 채널(&quot;모든 채널&quot;) 및 데이터가 통합된 MVPD에 대해 집계됩니다(&quot;모든 MVPD&quot;).

특정 옵션을 선택하지 않고 &quot;모든 채널&quot; 또는 &quot;모든 MVPD&quot;를 선택 취소하도록 선택하면 UI에 &quot;사용 가능한 데이터 없음&quot; 자리 표시자가 표시됩니다.


##### 보고서 내보내기 {#export-report}

모든 보고서를 사용하면 CSV(쉼표로 구분된 값) 형식 파일로 데이터를 내보낼 수 있습니다.

데이터를 내보내려면 창의 오른쪽 위 모서리에 있는 &quot;보고서 내보내기&quot; 단추를 사용하십시오. 그림 8 을 참조하십시오./9./10. 이미지 가져오기.

이름이 인 파일 **Report.csv** 컴퓨터에 자동으로 다운로드됩니다. 따라서 브라우저의 설정에서 파일을 다운로드할 수 있는지 확인하십시오.

Report.csv 파일이 계산되는 동안 &quot;데이터 내보내기&quot; 로드 아이콘이 화면에 표시됩니다. 이 아이콘을 통해 확인할 수 있습니다 **2~3분 정도** 내보낼 데이터 크기에 따라 다릅니다.

#### AuthN TTL 보고서(#authn-ttl-reports)

이 보고서는 모든 플랫폼에서 다양한 MVPD와 채널/s 통합을 위해 구성된 인증 토큰의 TTL(Time-To-Live)을 표시합니다.

인증 토큰 Time-To-Live라고도 합니다 **AuthN TTL**: **일, 시간, 분, 초**.

사용자 환경 측면에서 AuthN TTL 보고서를 사용하면 특정 MVPD 및 특정 플랫폼을 고려하여 사용자가 인증되는 시간을 시각적으로 확인할 수 있습니다.

이 유형의 보고서로 이동하려면 &quot;보고서&quot; 섹션에서 &quot;AuthN TTL 보고서&quot; 탭을 클릭하십시오.

![AuthN TTL 보고서](assets/authn-ttl-reports.png)

*그림 8: Adobe Primetime TVE 대시보드 AuthN TTL 보고서 탭*

AuthN TTL 보고서 테이블은 페이지를 포함하며 화면 크기에 따라 가로 및 세로 스크롤할 수 있습니다.

AuthN TTL 값을 변경하는 것을 고려할 경우 [통합](#tve-db-integrations-sec) 섹션을 참조하십시오.

>[!IMPORTANT]
>&quot;**MVPD에 의해 설정됨**&quot; 자리 표시자는 MVPD가 Adobe Primetime 인증 구성이 아니라 AuthN TTL 값을 적용하는 경우에 사용됩니다.


#### AuthZ TTL 보고서 {#authz-ttl-reports}

이 보고서는 모든 플랫폼에서 다양한 MVPD와 채널/s 통합을 위해 구성된 인증 토큰의 TTL(Time-To-Live)을 표시합니다.

인증 토큰 Time-To-Live라고도 합니다 **AuthZ TTL**: **일, 시간, 분, 초**.

사용자 환경 측면에서 AuthZ TTL 보고서를 사용하면 특정 MVPD 및 특정 플랫폼을 고려하여 사용자가 인증되는 시간을 시각적으로 확인할 수 있습니다.

이 유형의 보고서로 이동하려면 &quot;보고서&quot; 섹션에서 &quot;AuthZ TTL 보고서&quot; 탭을 클릭하십시오.

![AuthZ TTL 보고서](assets/authz-ttl-reports.png)

*그림 9. Adobe Primetime TVE 대시보드 AuthZ TTL 보고서 탭*

AuthZ TTL 보고서 테이블은 페이지를 포함하며 화면 크기에 따라 가로 및 세로 스크롤할 수 있습니다.

AuthZ TTL 값을 변경하는 것을 고려한다면 [통합](#tve-db-integrations-sec) 섹션을 참조하십시오.

>[!IMPORTANT]
>&quot;**MVPD에 의해 설정됨**&quot; 자리 표시자는 MVPD가 Adobe Primetime 인증 구성이 아니라 AuthZ TTL 값을 적용하는 경우에 사용됩니다.


#### SSO 보고서 {#sso-reports}

이 보고서는 모든 플랫폼에서 다양한 MVPD와 채널/s 통합에 대해 구성된 SSO(Single Sign-On) 상태를 표시합니다.

단일 사인온 상태라고도 합니다 **SSO 상태**&#x200B;는 다음 가능한 값이 있는 tri-state로 표시됩니다. **SSO 사용 안 함, SSO 사용, SSO 알 수 없음**.

사용자 환경 측면에서 SSO 보고서를 사용하면 특정 MVPD 및 특정 플랫폼을 고려하여 예상되는 사용자 인증 SSO 경험을 시각적으로 확인할 수 있습니다.

이 유형의 보고서로 이동하려면 &quot;**SSO 보고서**&quot; 탭에서&#x200B;**보고서**&quot; 섹션을 참조하십시오.


![TVE 대시보드 SSO 보고서 탭](assets/sso-reports.png)


*그림 10: Adobe Primetime TVE 대시보드 SSO 보고서 탭*

SSO 보고서 테이블에는 페이지가 있으며 화면 크기에 따라 가로 및 세로 스크롤이 가능합니다.

SSO 상태를 변경하는 것을 고려해 볼 경우 [통합](#tve-db-integrations-sec) 섹션을 참조하십시오.

>[!IMPORTANT]
>&quot;**SSO 미확인**&quot; 자리 표시자는 SSO가 활성화되어 있고 가능한 경우 사용되지만, 사용자 플랫폼 설정/사용자 결정(예: 타사 쿠키를 차단하는 사용자 브라우저 옵션, 사용자의 TV 공급자 구독 플랫폼 액세스를 거부하도록 선택한 사용자) 또는 MVPD 설정(예: 각 채널에 대해 인증을 요청하는 MVPD)이 SSO를 수행하지 못하도록 할 수 있습니다.

### 변경 로그 {#tve-db-changelog-sec}

이 섹션에는 TVE 대시보드를 통해 Adobe Primetime 인증 환경 및 구성에 푸시된 모든 수정 사항 목록이 표시됩니다.

푸시 날짜, 수정 작업을 수행한 사용자 및 푸시 상태를 나타내는 열이 있습니다.

또한 이 섹션에서는 검사하려는 특정 수정 사항을 좁히고 비교를 메일 항목으로 공유하는 두 테이블 항목을 비교할 수 있습니다.

### 피드백 {#tve-db-feedback-sec}

이 섹션에서는 피드백을 보낼 수 있습니다. 다음 단계에 따라 Adobe Primetime 인증 제품 팀에 피드백을 제공합니다.

* 화면 오른쪽에서 &quot;피드백&quot; 단추를 클릭합니다
* 제목 입력
* 메시지 입력
* 필요한 경우 &quot;스크린샷 업로드&quot; 단추를 클릭하여 메시지에 스크린샷을 업로드합니다.
* &quot;제출&quot; 단추 클릭

![대시보드 피드백 양식](assets/tve-dashboard-feedback.png)

*그림 11: Adobe Primetime TVE 대시보드 피드백 섹션*

스크린샷을 캡처하는 방법에 대한 지침은 아래 링크를 참조하십시오.

* [Windows에서 스크린샷을 캡처하는 방법](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b#1TC=windows-7)

* [Mac에서 스크린샷을 캡처하는 방법](https://support.apple.com/en-us/HT201361)

## 문제 해결 {#tve-db-troubleshoot}

### 유지 관리 모드 {#maintenance-mode}

![유지 관리 모드의 TVE 앱](assets/tveapp-maintenance-mode.png)


*그림: 유지 관리 모드의 TVE 앱*


TVE 대시보드가 &quot;유지 관리 모드&quot;인 경우 사용자는 새로운 변경을 보거나 수행할 수 없습니다.

이 경우 Adobe Primetime 인증 엔지니어링 팀이 TVE 대시보드에서 유지 관리 작업을 완료할 때까지 기다려야 합니다.

### 성능 저하 상태 {#degraded-state}

![성능이 저하된 상태의 TVE 앱](assets/tve-degraded-state.png)


*그림: 성능이 저하된 상태의 TVE 앱*

TVE 대시보드가 &quot;성능 저하 상태&quot;인 경우 사용자는 검색 및 정렬 기능이 없지만 사용자는 새로운 기능을 보거나 변경할 수 있습니다.

이 경우 Adobe Primetime 인증 엔지니어링 팀이 TVE 대시보드에서 유지 관리 작업을 완료할 때까지 기다려야 합니다.

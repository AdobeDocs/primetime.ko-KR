---
title: Safari 브라우저에 대한 JS SDK 제한 사항
description: Safari 브라우저에 대한 JS SDK 제한 사항
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Safari 브라우저에 대한 JS SDK 제한 사항 {#js-sdk-limitations-for-safari-browser}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

<!--
>[!IMPORTANT] 
>
>We are strongly recommending [migration to AccessEnabler JavaScript SDK versions 4.x](http://tve.helpdocsonline.com/accessenabler-js-v4-migration-guide) in order to have a stable and predictable behavior on Safari browser.-->


## 사파리 10 {#safari10}

**세부 사항**

* Safari 10부터 기본 브라우저 개인 정보 설정으로 인해 SSO(Single Sign-On), SLO(Single Logout) 및 수동 인증 기능이 작동하지 않습니다. 여러 탭이나 브라우저 창 간에 동일한 세션에서도 SSO(Single Sign-On) 및 수동 인증이 작동하지 않습니다.

* 이러한 변경 사항은 v2(버전 2.x), v3(버전 3.x), v4(버전 4.x)와 같은 AccessEnabler JavaScript SDK 버전에 대한 Adobe Primetime 인증 프로세스에 영향을 주며 영향을 줍니다.

### 완화 {#mitigation-safari10}

* 이러한 제한을 완화하려면 사용자에게 Safari 10 브라우저 개인 정보 설정을 변경하고 &quot;**항상 허용**&quot;옵션용&quot;**쿠키 및 웹 사이트 데이터**&quot;아래 이미지에 표시된 대로 환경 설정에서 브라우저의 개인 정보 탭에 있는 항목.

  ![](assets/always-allow-safari10.png)


## Safar 11 {#safari11}

**세부 사항**

>[!IMPORTANT]
>
>Safari 10 섹션의 위의 모든 세부 사항은 Safari 11의 경우에도 여전히 적용됩니다.

* Safari 11부터 브라우저는 다음을 도입합니다 [지능형 추적 방지](https://webkit.org/blog/7675/intelligent-tracking-prevention/)(ITP) 메커니즘으로, 사이트 간 추적을 방지하기 위해 휴리스틱을 사용하는 기술입니다. 이러한 휴리스틱은 네트워크 호출에서 타사 쿠키가 저장되고 재생되는 방식에 영향을 줍니다. 즉, ITP 메커니즘 활성화에 따라 Safari 브라우저는 클라이언트 - 서버 모델 통신에서 타사 쿠키를 차단합니다.

* Adobe Primetime 인증 서비스는 인증 프로세스의 일부로 쿠키를 사용하고 사용합니다 **기능을 하기 위하여**. 인증 프로세스가 자동으로 발생하는 상황(예: 임시 패스) 또는 iFrame 또는 &quot;리디렉션 불가&quot; 기능을 사용하는 구현에서 Adobe의 쿠키는 기본적으로 서드파티 쿠키로 간주되어 차단됩니다. 다른 모든 경우에 대해 Safari는 모든 Adobe의 Primetime 인증 서비스 쿠키를 추적 쿠키로 플래그 지정할 수 있는 머신 러닝 알고리즘을 사용하므로 ITP의 차단이 적용됩니다.

* 결론적으로, Safari 11 브라우저의 사용자는 ITP(Intelligent Tracking Prevention) 메커니즘을 활성화한 후, 특히 사용자가 여러 Adobe Primetime Authentication을 사용하는 웹 사이트를 사용하는 경우 Adobe Primetime 인증이 활성화된 웹 사이트에서 인증하지 못할 수 있습니다. 따라서 로그인 불능부터 예상 인증 기간보다 짧은 시간 등 사용자의 인증 경험이 예기치 않고 정의되지 않을 수 있습니다.

* 이러한 변경 사항은 v2(버전 2.x), v3(버전 3.x)과 같은 AccessEnabler JavaScript SDK 버전의 Adobe Primetime 인증 프로세스에 영향을 주며 영향을 줍니다.

### 완화 {#mitigation-safari11}

* AccessEnabler JavaScript SDK v3(버전 3.x)과 AccessEnabler JavaScript SDK v4(버전 4.x)의 경우 라이브러리에는 필수 쿠키가 누락되어 사용자 인증이 차단된 상황을 식별할 수 있는 메커니즘이 포함되어 있습니다. 이러한 경우 라이브러리는 특정 오류 콜백을 트리거합니다 [N](/help/authentication/error-reporting.md#advanced-error-codes-reference): Adobe Primetime 인증이 활성화된 웹 사이트로 다시 전달되어 사용자에게 문제를 완화할 수 있는 조치를 취하도록 지시하는 신호로 사용됩니다. 이 메커니즘을 활용하려면 웹 사이트에서 다음을 구현해야 합니다. [오류 보고](/help/authentication/error-reporting.md) 사양.

* AccessEnabler JavaScript SDK v2(버전 2.x)의 경우 라이브러리가 위에서 설명한 메커니즘을 제공하지 않으므로 Adobe Primetime 인증이 활성화된 웹 사이트에서 문제를 완화하기 위한 조치를 취하도록 사용자에게 지시할 때 신호를 보낼 수 없습니다.

* 앞서 언급한 문제를 완화할 수 있는 작업 목록 **세 버전 모두에 적용** AccessEnabler JavaScript SDK용

* 날짜 [N](/help/authentication/error-reporting.md#advanced-error-codes-reference) 오류 콜백이 구현자의 웹 사이트에서 수신되면, 사용자는 다음과 같이 ITP(Intelligent Tracking Prevention)를 비활성화하고 서드파티 쿠키를 사용하도록 설정해야 합니다.

* Mac OS X High Sierra 이상의 경우: &quot;**사이트 간 추적 방지**&quot; &quot;에 대한 옵션&#x200B;**웹 사이트 추적**&quot;아래 이미지에 표시된 대로 환경 설정에서 브라우저의 개인 정보 탭에 있는 항목.

  ![](assets/uncheck-prvnt-cr-st-tr-safari11.png)

* Mac OS X Sierra 및 이전 버전의 경우: &quot;**항상 허용**&quot;옵션용&quot;**쿠키 및 웹 사이트 데이터**&quot;아래 이미지에 표시된 대로 환경 설정에서 브라우저의 개인 정보 탭에 있는 항목.

  ![](assets/always-allow-safari11.png)

## 사파리 12 {#safari12}

**세부 사항**

>[!IMPORTANT]
>
>섹션 Safari 10 및 섹션 Safari 11의 위의 모든 세부 사항은 Safari 12의 경우에도 여전히 적용됩니다.

이 섹션에서는 의 호환성 문제에 대해 자세히 설명합니다. **AccessEnabler JavaScript SDK 버전 4.x** safari 12에서.

>[!NOTE]
>
>AccessEnabler JavaScript SDK 버전 2.x 및 AccessEnabler JavaScript SDK 버전 3.x의 경우 둘 다 인증 프로세스에 타사 쿠키를 사용하며, Safari 11부터 시작되는 ITP 및 타사 쿠키 정책으로 인해 로그인 불능에서 예상 인증 기간보다 짧은 시간에 이르기까지 사용자의 인증 경험이 예기치 않고 정의되지 않을 수 있다는 점을 염두에 두십시오.


### Safari 12에서 AccessEnabler JavaScript SDK v4(버전 4.x)의 인증된 기능 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

* **인증** 버전 4.0부터 AccessEnabler JavaScript SDK는 인증 프로세스에 더 이상 서드파티 쿠키를 사용하지 않으므로 사용자의 브라우저에서 서드파티 쿠키가 비활성화되어 있더라도, 사용자 상호 작용을 사용하는 흐름은 항상 작동합니다.

>[!NOTE]
>
>사용자는 로그인 팝업을 열거나 MVPD 로그인 페이지와 상호 작용하려면 사이트와 상호 작용해야 합니다.

* **Authorization/Preflight/User 메타데이터** 사용자가 이미 인증된 경우 작업이 완전히 작동합니다.

### Safari 12에서 AccessEnabler JavaScript SDK v4(버전 4.x)의 알려진 문제 {#known-issues-of-accessenabler-javascript-sdk-4}

* SSO 및 SLO

   * Safari 10부터 Safari에서 localStorage가 구현되는 방식으로 인해 JS SDK는 더 이상 공통 도메인 iFrame을 통해 로그인 상태를 공유할 수 없습니다. 즉, AccessEnabler JavaScript SDK를 사용하는 모든 사이트에 로그인해야 합니다. 또한 로그아웃해도 사이트 간에 인증 토큰이 삭제되지 않으므로 사용자는 Adobe Primetime 인증이 활성화된 각 웹 사이트에서 로그아웃해야 합니다.

* 임시 통과

   * 임시 전달의 경우 AccessEnabler JavaScript SDK는 개별화 메커니즘을 사용하여 인증 토큰을 특정 디바이스(브라우저 인스턴스)에 잠급니다. 추적을 방지하기 위해 설계된 Safari 12의 새로운 메커니즘으로 인해, 우리가 개별화 메커니즘에서 계산하고 사용하는 지문은 **은(는) 동일한 IP 주소를 가진 모든 사용자에 대해 동일합니다**. 우리는 개별화 목적을 위해 클라이언트 IP를 고려하지만, 그럼에도 불구하고 동일한 공개 IP 주소를 공유하는 사용자들에게 영향을 미칩니다. 이러한 사용자의 경우 동일한 개별화 ID를 계산하고 임시 패스가 여기에 연결됩니다. 즉, 이러한 사용자가 임시 패스를 사용하면 다른 사용자는 해당 패스에 액세스할 수 없습니다. \! 이는 특히 기업 사용자, 교육 기관 또는 인터넷에 액세스하기 위해 NAT 또는 공통 프록시를 사용하는 여러 사용자가 있는 기타 조직에 영향을 미칩니다.

>[!NOTE]
>
>이 문제는 구현자가 사용자 상호 작용의 결과로 임시 패스를 사용하는 경우에만 사용자에게 영향을 미칩니다. 그렇지 않으면 임시 패스 인증의 대상이 됩니다. **자동 흐름** 아래요.

* 자동 흐름

   * JS SDK 4.0을 사용하는 경우 사용자 상호 작용 없이 자동화된 모드로 인증 흐름을 시도하면 Safari 12에서 성공하지 못합니다. 예정된 JS SDK 4.1에서는 자동화된 흐름의 모든 문제를 해결합니다.

이 문제의 영향을 받는 사용 사례:

* 자동 TempPass(무료 미리 보기) 인증 - 이러한 흐름의 경우 SDK에서 N130 오류가 발생합니다.

* 수동 인증(자동으로 실패) - 이 MVPD를 선택하고 자격 증명을 입력하라는 메시지가 표시됩니다.

### 완화 {#mitigation-safari12}

**SSO 및 SLO**

이 글을 쓰는 순간에 이용 가능하거나 가능한 알려진 완화는 없다. Apple은 Safari 12에 &quot;스토리지 액세스 API&quot;를 도입했습니다(`https://webkit.org/blog/8124/introducing-storage-access-api`), 하지만 현재 구현은 localStorage에는 적용되지 않고 쿠키에만 적용됩니다. 또한 API를 사용하려면 사용자 상호 작용이 필요하며, API를 사용하면 아래 대화 상자와 유사한 권한 대화 상자가 표시됩니다.

![](assets/permission-dialog-apple.png)


이 시점에서는 이러한 Safari 요구 사항/프롬프트가 UX 요구 사항과 일치하지 않으며, 다른 브라우저에서와 같이 일관된 비헤이비어가 없습니다. 여기서 SSO는 일단 공통 도메인 localStorage에 토큰을 저장하면 &quot;작동&quot;합니다.

**임시 통과**

개별화 문제를 완화하고 사용자 상호 작용을 하기 위해 다음을 사용하는 것이 좋습니다. **[프로모션 임시 패스](/help/authentication/promotional-temp-pass.md)** 대화식 방법으로, 사용자에게 하나 이상의 추가 정보(예: 이메일 주소)를 제공합니다.

## 사파리 13 {#safari13}

**세부 사항**

>[!IMPORTANT]
>
>섹션 Safari 10부터 섹션 Safari 12까지 위의 모든 세부 사항은 Safari 13의 경우에도 여전히 적용됩니다.


Safari 13부터 브라우저는 [지능형 추적 방지](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP), 사이트 간 추적을 방지하기 위해 서드파티 쿠키를 추적 쿠키로 플래그를 지정하는 과정에서 메커니즘의 추론을 더 엄격하게 만듭니다.

이전 섹션에서 설명한 바와 같이 Adobe Primetime 인증 서비스는 구현자가 AccessEnabler JavaScript SDK v2(버전 2.x) 및 AccessEnabler JavaScript SDK v3(버전 3.x)을 사용할 때 인증 프로세스의 일부로 타사 쿠키를 사용하고 사용합니다. ITP가 사용자와 관련 당사자(프로그래머의 웹 사이트 및 Adobe) 간의 상호 작용에 대해 &quot;학습&quot;하기 위해 잠시 후에 시작된 Safari 브라우저의 이전 버전과 비교하여 Safari 13 브라우저는 클라이언트 - 서버 모델 통신에서 쿠키를 추적하는 것으로 간주되는 타사 쿠키를 처음부터 차단하고 있습니다.

결론적으로, Safari 13 브라우저의 사용자는 이전 버전의 AccessEnabler JavaScript SDK, v2(버전 2.x) 또는 v3(버전 3.x)을 사용하는 Adobe Primetime 인증이 활성화된 웹 사이트에서 새로운 인증을 시작할 수 없을 것입니다. 이는 필요한 모든 Adobe의 Primetime 인증 서비스 쿠키가 ITP에 의해 차단되므로 서비스가 인증 요청을 이행할 수 없기 때문에 발생합니다.

AccessEnabler JavaScript SDK v4(버전 4.x) 라이브러리는 인증 프로세스에 타사 쿠키를 사용하지 않으므로 Safari 13 변경 사항의 영향을 받지 않습니다.

### 완화 {#mitigation-safari13}

무엇보다도 저희는 강력히 추천합니다 **AccessEnabler JavaScript SDK 버전 4.x로 마이그레이션** safari 브라우저에서 안정적이고 예측 가능한 동작을 할 수 있습니다.

두 번째로, AccessEnabler JavaScript SDK v3(버전 3.x)의 경우, 라이브러리에는 필수 쿠키가 누락되어 사용자 인증이 차단된 상황을 식별할 수 있는 메커니즘이 포함되어 있습니다. 이러한 경우 라이브러리는 특정 오류 콜백([N](/help/authentication/error-reporting.md#advanced-error-codes-reference))를 참조하십시오. 이 값은 문제를 완화할 수 있는 작업을 사용자에게 지시하기 위한 신호로 사용하기 위해 Adobe Primetime 인증이 활성화된 웹 사이트로 다시 전달됩니다. 이 메커니즘을 활용하려면 웹 사이트에서 다음을 구현해야 합니다. [오류 보고](/help/authentication/error-reporting.md) 사양.

AccessEnabler JavaScript SDK v2(버전 2.x)의 경우 라이브러리가 위에서 설명한 메커니즘을 제공하지 않으므로 Adobe Primetime 인증이 활성화된 웹 사이트에서 문제를 완화하기 위한 조치를 취하도록 사용자에게 지시할 때 신호를 보낼 수 없습니다.

날짜 [N](/help/authentication/error-reporting.md#advanced-error-codes-reference) 오류 콜백이 구현자의 웹 사이트에서 수신되면, 사용자는 다음과 같이 ITP(Intelligent Tracking Prevention)를 비활성화하고 서드파티 쿠키를 사용하도록 설정해야 합니다.

* Mac OS X High Sierra 이상의 경우: &quot;**사이트 간 추적 방지**&quot; &quot;에 대한 옵션&#x200B;**웹 사이트 추적**&quot;아래 이미지에 표시된 대로 환경 설정에서 브라우저의 개인 정보 탭에 있는 항목.

  ![](assets/prvnt-cross-site-tr-safari13.png)

* Mac OS X Sierra 및 이전 의 경우: 확인 t</span>그 &quot;**항상 허용**&quot;옵션용&quot;**쿠키 및 웹 사이트 데이터**&quot;아래 이미지에 표시된 대로 환경 설정에서 브라우저의 개인 정보 탭에 있는 항목.

  ![](assets/always-allow-safari13.png)

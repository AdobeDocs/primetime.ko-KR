---
title: 어디에서나 TV를 위한 홈 기반 인증
description: 어디에서나 TV를 위한 홈 기반 인증
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---


# 어디에서나 TV를 위한 홈 기반 인증

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 홈 기반 인증이란 무엇입니까? {#whatis-home-based-authn}

HBA(Home Based Authentication)는 TV Everywhere 기능으로, 유료 TV 가입자들이 집에 있을 때 MVPD 자격 증명을 입력하지 않고도 온라인으로 TV 컨텐츠를 볼 수 있도록 함으로써 인증 흐름의 사용자 경험을 크게 향상시킬 수 있습니다.

개방형 인증 기술 위원회(OATC)의 홈 기반 인증 정의: &quot;홈 자동 인증은 MVPD/OVD가 홈 네트워크의 특성(또는 홈 네트워크의 장치 간에 자동으로 액세스할 수 있는 식별자)을 사용하여 해당 홈 네트워크에 연결된 가입자 계정을 인증함으로써 TVE 보호 컨텐츠에 액세스하기 위한 TVE 세션을 설정할 때 사용자가 자격 증명을 수동으로 입력할 필요가 없는 프로세스입니다.&quot;



HBA 및 업계 표준에 대한 자세한 내용은 [OATC 사용 사례 및 요구 사항](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} 설명서 및 **HBA에 대한 OATC 사용자 환경 지침**.

>[!NOTE]
>
>일부 HBA 흐름은 Premium Workflow 패키지의 일부입니다. 이 기능을 사용하려면 Primetime 영업 담당자에게 문의하십시오.

## HBA가 중요한 이유 {#why-hba}

HBA는 집에 있고 이미 케이블 가입되어 있는 뷰어의 로그인 장벽을 실제로 제거하기 때문에 중요합니다. 또한 홈 기반 인증은 뷰어의 참여를 크게 향상시키고 TV Everywhere 콘텐츠를 위한 더 나은 사용자 경험을 제공할 수 있습니다.

현재, 로그인 시도 중 거의 절반이 성공하지 못했습니다.

상위 5개 MVPD 중 하나에 의해 HBA가 활성화되면 인증 전환율이 적용됩니다 **40% 증가** (45%에서 63%로)

![](assets/authn-conv-pre-post.png)

또한 아래에서는 다른 MVPD와 통합된 채널에 대한 로그인 전환율을 볼 수 있습니다. HBA를 사용할 수 있는 HBA와 HBA가 없는 HBA HBA를 사용하는 경우 HBA가 없는 경우보다 전환율이 훨씬 높습니다.

![](assets/hba-vs-non-hba.png)

이 MVPD와 통합된 대부분의 채널에 대해 HBA를 활성화한 후 6개월이 지난 후 고유 사용자가 82% 증가한 것을 발견했습니다(이 MVPD를 통해 TV Everywhere 채널에 액세스하는 사용자 수는 두 배가 되었습니다.).

2w3반면에 아래 차트에서 볼 수 있듯이 HBA를 활성화하지 않은 다른 MVPD는 지난 6개월 동안 고유 사용자가 26% 증가했을 뿐입니다.

![](assets/unique-visitors-incr.png)

HBA를 활성화한 후 6개월 전과 6개월 동안 수집된 데이터에서 HBA가 활성화된 채널에 대한 시청자 참여도가 크게 향상되었습니다. HBA가 활성화된 MVPD 사용자는 HBA가 설정되지 않은 MVPD의 사용자보다 평균 30% 더 많은 컨텐츠를 보는 경향이 있습니다.

![](assets/user-engagement-increase.png)

## Primetime 인증 HBA 지원 {#auth-hba-support}

이 섹션에서는 Primetime 인증에서 제공하는 HBA 지원, HBA 흐름에서 Primetime 인증 플랫폼의 동작 및 HBA 구현에 유용한 기술 세부 정보를 제공합니다.

HBA를 지원하는 Primetime 인증 기능

* HBA와 비HBA 인증과 HBA에 대해 서로 다른 인증 TTL을 설정하는 기능(MVPD 지원 필요)
* 인증이 만료된 경우 MVPD(MVPD 선택기 건너뛰기)를 자동으로 선택할 수 있습니다. 이는 특히 HBA TTL이 작은 경우에 유용합니다.
* 인증이 HBA이거나 그렇지 않은 경우 프로그래머에게 노출할 수 있습니다(또한 MVPD 지원 필요).

### Primetime 인증 플랫폼의 HBA 사용자 경험 {#hba-user-exp}

다음 표는 HBA가 활성화되고 HBA가 활성화되지 않은 경우 지원되는 플랫폼에 대한 사용자 환경에 대한 정보를 제공합니다.

| 사용자 흐름 - 플랫폼 유형 | swf, iOS, Android |
|---|---|
| HBA 사용 | 사용자가 집에 있으면 자동으로 인증됩니다. HBA AuthN 토큰이 만료되면 사용자가 자동으로 다시 인증됩니다. |
| HBA 제외 | 사용자는 MVPD를 선택하고 자신의 자격 증명을 입력하라는 메시지가 표시됩니다. AuthN 토큰이 만료되면 사용자는 자격 증명을 다시 입력해야 합니다. |

| 사용자 흐름 - 플랫폼 유형 | js, Windows(기본) |
|---|---|
| HBA 사용 | 사용자가 집에 있으면 자동으로 인증됩니다. HBA AuthN 토큰이 만료되면 사용자는 선택기에서 MVPD를 다시 선택해야 하며 자동으로 인증됩니다. |
| HBA 제외 | MVPD를 선택하고 자격 증명을 입력하도록 사용자에게 홈에 있더라도 권고합니다. AuthN 토큰이 만료되면 사용자가 자격 증명을 다시 입력해야 합니다. |

| 사용자 흐름 - 플랫폼 유형 | Clientless REST API(두 번째 화면 인증) |
|---|---|
| HBA 사용 | 사용자가 집에 있고 Clientless REST API 앱을 사용하는 경우 등록 코드를 입력하고 MVPD를 선택하면 두 번째 화면 장치에서 자동으로 인증됩니다. HBA AuthN 토큰이 만료되면 사용자는 자동으로 다시 인증됩니다(두 번째 화면 장치에서). |
| HBA 제외 | MVPD를 선택하고 자격 증명을 입력하도록 사용자에게 홈에 있더라도 권고합니다. AuthN 토큰이 만료되면 사용자가 자격 증명을 다시 입력해야 합니다. |

### HBA 구현에 대한 기술 세부 정보 {#tech-details-hba}

#### OAuth 2.0 프로토콜 {#oauth-2-protocol}

OAuth 2.0 인증 프로토콜과 통합된 MVPD의 HBA 플로우에서 MVPD는 새로 고침 토큰을 발급하고 HBA 인증 토큰에 Adobe이 발생합니다.

* 새로 고침 토큰은 MVPD의 비즈니스 요구 사항에 의해 결정된 TTL입니다.
* HBA 인증 토큰 TTL **작거나 같아야 합니다.** 새로 고침 토큰 TTL입니다.


*OAuth 2.0 프로토콜에 대한 HBA 인증 흐름에 대한 설명입니다*


| 사용자 작업 | 시스템 작업 |
|---|---|
| 사용자가 프로그래머 사이트로 이동합니다. 비디오를 재생하려고 하면 MVPD 선택기가 표시됩니다. 사용자가 MVPD를 선택하고 로그인을 클릭합니다. | 신원 확인이 수행됩니다. MVPD는 사용자 검색에 대한 규칙 세트를 적용합니다(예를 들어, 사용자의 IP 주소를 배포자가 프로비저닝된 모뎀의 MAC 주소 또는 광대역 연결 셋톱 박스)에 매핑합니다. |
| 약 3초 동안 지속되는 화면이 표시됩니다. 사용자에게 MVPD 계정을 사용하여 자동으로 로그인한다는 알림을 받는 삽입 광고 페이지가 표시될 수 있습니다. | <ol><li>프로그래머 측에 설치된 AccessEnabler는 인증 요청(HTTP 요청)을 Adobe Primetime 인증 끝점으로 보냅니다.</li><li>Primetime 인증 종단점은 요청을 MVPD 인증 종단점으로 리디렉션합니다. <br />**참고:** 이 요청에는 다음이 포함되어 있습니다 `hba_flag` MVPD가 HBA 인증을 시도해야 함을 알리는 매개 변수(시도 HBA = true)입니다.</li><li>MVPD 인증 끝점이 Adobe Primetime 인증 끝점에 인증 코드를 보냅니다.</li><li>Adobe Primetime 인증은 인증 코드를 사용하여 MVPD의 토큰 끝점에서 새로 고침 토큰 및 액세스 토큰을 요청합니다.</li><li>MVPD가 인증 결정 및 `hba_status` (true/false) 매개 변수를 `id_token`.</li><li>MVPD 사용자 프로필 끝점에 대한 호출이 전송되어 [사용자 메타데이터의 hba_status 키](/help/authentication/user-metadata-feature.md#obtaining).</li><li>MVPD는 새로 고침 토큰 TTL을 MVPD가 동의한 값으로 설정하고 Adobe은 AuthN 토큰 TTL을 새로 고침 토큰의 값과 작거나 같은 값으로 설정합니다.</li></ol> |
| 사용자가 인증되었으며 이제 권한 있는 TV Everywhere 콘텐츠를 검색할 수 있습니다. | 이제 프로그래머의 사이트를 검색할 수 있는 사용자에게 인증 토큰이 전달됩니다. |

#### SAML 프로토콜 {#saml-protocol}

SAML 인증 프로토콜에 대한 HBA 인증 흐름에 대한 설명

| 사용자 작업 | 시스템 작업 |
|---|---|
| 사용자가 프로그래머 사이트로 이동합니다. 비디오를 재생하려고 하면 MVPD 선택기가 표시됩니다. 사용자가 MVPD를 선택하고 로그인을 클릭합니다. | 신원 확인이 수행됩니다. MVPD는 사용자 검색에 대한 규칙 세트를 적용합니다(예를 들어, 사용자의 IP 주소를 배포자가 프로비저닝된 모뎀의 MAC 주소 또는 광대역 연결 셋톱 박스)에 매핑합니다. |
| 약 3초 동안 지속되는 화면이 표시됩니다. 사용자에게 MVPD 계정을 사용하여 자동으로 로그인한다는 알림을 받는 삽입 광고 페이지가 표시될 수 있습니다. | <ol><li>프로그래머 측에 설치된 AccessEnabler는 인증 요청(HTTP 요청)을 Adobe Primetime 인증 끝점으로 보냅니다.</li><li>Primetime 인증 종단점은 요청을 MVPD 인증 종단점으로 리디렉션합니다.</li><li>MVPD는 HBA 플래그를 포함해야 하는 SAML 응답 형식으로 인증 결정을 보내야 합니다. hba_status (true/false)</li><li>MVPD 사용자 프로필 끝점에 대한 호출이 전송되어 [사용자 메타데이터의 hba_status 키](/help/authentication/user-metadata-feature.md#obtaining).</li></ol> |
| 사용자가 인증되었으며 이제 권한 있는 TV Everywhere 콘텐츠를 검색할 수 있습니다. | 이제 프로그래머의 사이트를 검색할 수 있는 사용자에게 인증 토큰이 전달됩니다. |


## HBA 활성화 방법 {#how-to-activate-hba}

* **OAuth 프로토콜:**
   * HBA를 사용하려면 다음을 참조하십시오. [Primetime TVE 대시보드 사용 안내서](/help/authentication/tve-dashboard-user-guide.md)
* **SAML 프로토콜:** 홈 기반 인증이 MVPD 측에서 활성화됩니다. 프로그래머 또는 Adobe은 작업을 수행할 필요가 없습니다.
홈 기반 인증을 지원하는 MVPD에 대한 자세한 내용은 [MVPD에 대한 HBA 상태](/help/authentication/hba-status-mvpds.md).

## FAQ {#faqs}


**질문:** SAML과 OAuth2 프로토콜을 사용한 홈 기반 인증을 구분하는 이유는 무엇입니까?

**답변:** HBA 흐름은 두 프로토콜에 대해 다릅니다. 프로그래머의 관점에서 HBA는 SAML MVPD에 대해 활성화되도록 할 필요가 없지만 OAuth2 MVPD의 경우 Primetime TVE 대시보드에서 HBA를 켜거나 끌 수 있습니다.



**질문:** HBA가 활성화될 때 처음 인증할 때 사용자 이름과 암호를 입력해야 합니까?

**답변:** 아니요, 사용자 이름과 암호는 필요하지 않습니다.



**질문:** 자녀 보호를 어떻게 실시합니까?

**답변 1:** Adobe은 유해 컨텐츠 제어 승인이 필요한 채널과의 통합을 위해 HBA를 비활성화할 수 있습니다.

**답변 2:** Adobe은 UX 문서에서 OATC를 사용하여 자녀 보호 기능을 사용하여 HBA 환경을 설정하는 방법을 권장합니다.



**질문:** HBA를 지원하는 공급자가 HBA에 대해 TTL 기간이 더 짧습니까? 그러면 일반 인증에 대해 HBA를 지원합니까?

**답변:** TTL 설정은 구성할 수 있습니다. 잘못 처리되지 않도록 HBA 인증 토큰에 대해 짧은 TTL을 설정하는 것이 좋습니다.


## 유용한 정보 {#useful-info}

* [HBA(Instant Access) Recommendations](http://www.ctamtve.com/instantaccess){target=_blank} - CTAM 기준
* [프로그래머 앱에서 HBA 구현 샘플](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/HBA_Flow_Sample.pdf?dc=201604222139-1346){target=_blank} - Adobe 기준
   <!--* [Home Based Authentication User Experience Guidelines for TV Everywhere](http://oatc.us/Standards/DownloadRecommendedPractices.aspx){target=_blank} - by OATC-->
* [홈 기반 인증 사용 사례 및 요구 사항](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} OATC에 의해
* [홈 기반 인증 정보](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf?dc=201604260953-2640){target=_blank} - Adobe 기준
* [OAuth 2.0 프로토콜을 사용한 인증](/help/authentication/authn-oauth2-protocol.md)
* [SAML MVPD를 사용한 인증](/help/authentication/authn-usecase.md)
* [Primetime TVE 대시보드 사용 안내서](/help/authentication/tve-dashboard-user-guide.md)
* [hba_status 사용자 메타데이터](/help/authentication/user-metadata-feature.md#obtaining)




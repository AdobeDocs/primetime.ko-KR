---
title: 용어 설명
description: 용어 설명
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# 용어 설명 {#glossary}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## AccessEnabler {#accessEnabler}

Adobe Primetime 인증의 클라이언트 구성 요소입니다. Adobe Primetime 인증에서는 지원되는 플랫폼마다 AccessEnabler 라이브러리를 제공합니다.

## AuthN {#authn}

&quot;AuthN 토큰&quot; 또는 &quot;AuthN 흐름&quot;과 같이 &quot;인증&quot;의 축약어로 사용됩니다.


## AuthN 토큰{#authn-token}

사용자가 MVPD로 인증되면 Adobe Primetime 인증에서 생성된 인증 토큰. 프로그래머의 통합 플랫폼에 따라 토큰은 사용자의 장치 또는 Adobe Primetime 인증 서버에 저장됩니다.

## AuthZ {#authz}

&quot;AuthZ 토큰&quot; 또는 &quot;AuthZ 흐름&quot;과 같이 &quot;인증&quot;의 축약어로 사용됩니다.

## AuthZ 토큰 {#authz-token}

사용자가 보호된 콘텐츠를 볼 수 있는 권한이 부여된 후 Adobe Primetime 인증에서 생성된 인증 토큰. AuthZ 토큰은 Adobe Primetime 인증 서버에 저장되며 [단기 미디어 토큰](#short-lived-token).

## 채널 ID(더 이상 사용되지 않음) {#channel_id}

리소스 ID의 이전 용어입니다.

## Clientless API {#clientless-api}

AccessEnabler 클라이언트 구성 요소 대신 웹 서비스를 사용하는 Adobe Primetime 인증 통합 솔루션입니다.

## 장치 ID {#device-id}

장치(예: 전화, 태블릿 등)를 고유하게 식별합니다 Adobe Primetime 인증 내에서 사용할 수 있습니다. 이 ID는 Programmer의 애플리케이션에서 획득/제공합니다.


## 자격 흐름{#entitlement_flow}

Adobe Primetime 인증 설명서에서 사용하는 용어는 장치/사용자를 Adobe Primetime 인증에 등록하고, MVPD로 사용자를 인증하며, 사용자에 대한 리소스를 인증하고, 사용자를 로그아웃하는 전체 프로세스를 의미합니다.


## GUID {#guid}

자세한 내용은 [사용자 ID](#user-id).

## IdP {#idp}

공급자 식별 Adobe Primetime 인증 통합에서 MVPD의 역할 컨텍스트에서 MVPD와 동의됩니다. (고객은 유료 TV 공급자의 로그인 페이지를 통해 자신의 ID를 확인해야 합니다.)

## 미디어 토큰 확인 프로그램 {#media-token-verifier}

자격 부여 흐름이 성공적으로 완료된 후 Adobe Primetime 인증에서 생성된 단기 미디어 토큰을 확인하는 데 프로그래머가 사용하는 Adobe 제공 라이브러리입니다.

## MVPD {#mvpd}

다채널 비디오 프로그래밍 배포자 유료 TV 제공자와 동의어.

## MVPD ID {#mvpd-id}

자세한 내용은 [사용자 ID](#user-id).

## 파트너 ID {#partner-id}

Adobe이 MVPD에 전달하는 식별자로, 이 식별자를 사용하여 인증을 요청하는 대리 Adobe Primetime 인증을 식별하는 데 사용됩니다. 경우에 따라 특정 프로그래머용 UI를 구성하는 데 사용되고, 경우에 따라 모든 프로그래머에서 동일하며 MVPD의 필요에 따라 다릅니다.

## 유료 TV 공급자 {#pay-tv-provider}

와 동의어 [MVPD](#mvpd).

## 프로그래머 {#programmer}

&quot;컨텐츠 공급자&quot;, &quot;계정&quot;, &quot;채널&quot;, &quot;서비스 공급자&quot;, &quot;브랜드&quot; 등과 동의됩니다.

## 프록시 MVPD {#proxy-mvpd}

다른 MVPD에 대한 ID 서비스를 제공하는 MVPD; Adobe Primetime 인증과 직접 통합

## 프록시 MVPD {#proxied-mvpd}

Adobe SP와 직접 통합되지 않지만 프록시 MVPD를 통해 통합된 MVPD입니다.

## 요청자 ID {#requestor-id}

고유하게 식별 [프로그래머](#programmer) (Adobe Primetime 인증 내의 계정, 브랜드, 채널 또는 속성). 이 ID는 계정의 초기 설정 중에 프로그래머와 Adobe 간에 결정됩니다. 웹에서 요청자 ID는 화이트리스트에 추가한 도메인 세트와 연결됩니다. 외부 도메인에서 ID를 사용하는 모든 호출은 거부됩니다. 프로그래머도 분석에 요청자 ID를 사용합니다. 일반적으로 프로그래머당 요청자 ID는 하나만 있습니다. 요청자 ID와 관련된 한 가지 추가 기능은 setRequestor API 호출에서 Adobe Primetime 인증 시스템에서 프로그래머를 인증하는 데 사용되는 암호화된 데이터를 전송해야 하므로 Adobe이 공개 인증서를 제공해야 한다는 것입니다.

## 리소스 ID {#resource-id}

를 식별하는 문자열 또는 mRSS 리소스 [프로그래머](#programmer) MVPD에 추가합니다. 그것은 프로그래머와 MVPD가 합의한 것이다. Adobe Primetime 인증은 리소스 ID를 그대로 통과하므로 모든 MVPD에 대해 동일해야 합니다. MVPD가 각 ID가 나타내는 것을 알고 있는 한 프로그래머는 여러 리소스 ID를 사용할 수 있습니다.

## SessionGUID {#sessionGUID}

자세한 내용은 [사용자 ID](#user-id).

## 단기 미디어 토큰 {#short-lived-token}

이 토큰은 특정 사용자에 대한 자격 프로세스가 성공적으로 완료되면 Adobe Primetime 인증에 의해 생성됩니다. 토큰이 Programmer에 전달됩니다. Programmer는 단기 미디어 토큰에서 Adobe Primetime 인증 토큰 확인기를 사용하여 자격 프로세스의 보안을 확인합니다.

## 스마트 장치 {#smart-device}

Adobe Primetime 인증 설명서 전체에서 사용되는 용어로서 셋톱 박스, 게임 콘솔 및 스마트 TV를 참조합니다. 이러한 장치는 네트워킹 기능이 있지만 웹 페이지를 렌더링할 수 없는 장치입니다.

## SP{#sp}

서비스 공급자 일반적으로 *역할* Adobe Primetime 인증에서 재생되는 SP에서 [MVPD](#mvpd).

## 임시 통과 {#temp-pass}

프로그래머가 유료 컨텐츠에 대한 임시 무료 액세스를 제공할 수 있는 기능입니다. Programmer가 지정한 기간 동안 Access는 요청자마다 다릅니다.

## TTL {#ttl}

살 시간입니다. 토큰이 유효한 지정된 기간입니다.

## TVE {#tve}

TV는 어디에나 있습니다.

## 사용자 ID {#user-id}

프로그래머 앱의 사용자를 고유하게 식별하지만 MVPD에서 구성됩니다. 다양한 사용 사례에 대해 다른 양식에서 사용할 수 있습니다. 자세한 내용은 [프로그래머 개요의 사용자 ID 이해](/help/authentication/programmer-overview.md#user-ids).

## 허용 목록 {#whitelist}

Adobe Primetime 인증과 통신하기 위해 합법으로 지정된 도메인 목록입니다.

## XSTS 토큰 {#xsts-token}

Xbox/Adobe Primetime 인증 통합에서 사용되는 Xbox 콘솔 앱 개발용 Microsoft에서 발행한 보안 토큰입니다.

---
title: 서버측 지표 이해
description: 서버측 지표 이해
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 0%

---

# 서버측 지표 이해 {#understanding-server-side-metrics}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.


## 소개 {#intro}

이 문서에서는 ESM(자격 서비스 모니터링) 서비스에서 생성한 Adobe Primetime 인증 서버측 지표에 대해 설명합니다. 클라이언트측 관점에서 볼 때 동일한 이벤트(프로그래머가 페이지/애플리케이션에서 Adobe Analytics과 같은 측정 서비스를 구현할 경우 보게 되는 이벤트)는 설명하지 않습니다.

## 이벤트 요약 {#events_summary}

Adobe Primetime 인증 서버측 관점에서 다음 이벤트가 생성됩니다.

* **인증 흐름에서 생성된 이벤트**(MVPD를 사용한 실제 로그인)

   * AuthN 시도 알림 - 사용자가 MVPD 로그인 사이트로 전송될 때 생성됩니다.
   * AuthN 보류 중 알림 - 사용자가 MVPD로 로그인하는 데 성공하면 사용자가 Primetime 인증으로 다시 리디렉션될 때 생성됩니다.
   * AuthN Granted 알림 - 사용자가 프로그래머 사이트로 돌아가 Primetime 인증에서 인증 토큰을 성공적으로 검색했을 때 생성됩니다.
* **인증 흐름** (MVPD에 대한 인증만 확인)\
  *전제 조건:* 유효한 AuthN 토큰
   * AuthZ 시도 알림
   * AuthZ 알림 부여됨
* **재생 요청 성공**\
  *전제 조건:* 유효한 AuthN 및 AuthZ 토큰
   * Adobe Primetime 인증을 사용한 검사 알림
   * 재생 요청에는 부여된 인증과 부여된 인증이 모두 필요합니다


고유 사용자의 수는 [고유 사용자](#unique-users) 아래 섹션. 개요로서 부여된 인증 및 권한 부여 응답은 일반적으로 캐시되므로 일반적으로 다음 공식이 적용됩니다.

* AuthN 시도 횟수 \> 부여된 AuthN 횟수
* AuthZ 시도 횟수 \> 부여된 AuthZ 횟수
* AuthZ 시도 횟수 \> 부여된 AuthN 횟수(일반적으로)
* 성공한 재생 요청 수 \> 부여된 AuthZ 수


### 예 {#example}

다음 예는 한 브랜드에 대한 1개월의 서버측 지표를 보여줍니다.

| 지표 | MVPD 1 | MVPD 2 | … | MVPD n | 합계 |
| -------------------------- | ------ | ------ | - | ------ | ---------------------------------------------- |
| 성공한 인증 | 1125 | 2892 |   | 2203 | SUM(MVP1+...MVPD n) |
| 성공한 승인 | 2527 | 5603 |   | 5904 | SUM(MVP1+...MVPD n) |
| 성공한 재생 요청 | 4201 | 10518 |   | 10737 | SUM(MVP1+...MVPD n) |
| 고유 사용자 | 1375 | 2400 |   | 2890 | 중복 제거된 모든 MVPD에 대한 모든 사용자 합계\* |
| 시도된 인증 | 2147 | 3887 |   | 3108 | SUM(MVP1+...MVPD n) |
| 시도된 승인 | 2889 | 6139 |   | 6039 | SUM(MVP1+...MVPD n) |

</br>

이 경우 중복 제거는 다른 MVPD 사용자가 동일한 사용자 ID를 받지 않아야 하므로 영향을 주지 않습니다. 서로 다른 두 브랜드의 합계를 만들 때 동일한 MVPD를 사용하면 중복 제거 효과가 훨씬 커집니다.

## 이벤트 트리거 {#event_triggers}

### 새 사용자 - 전체 흐름 {#new-user-full-flow}

다음 차트는 인증 토큰이 없는 사용자(새 사용자 또는 인증 토큰이 만료된 사용자)에 대한 이벤트 및 단계에 대해 설명합니다.



![](assets/ae-flow-with-events.png)



이 흐름에는 인증(\#7에 #5)과 인증(\#11) 모두에 대해 MVPD로 이동하는 작업이 포함됩니다.



흐름이 완료되면 인증 및 권한 부여 토큰이 사용자의 장치에 캐시됩니다. 인증 토큰의 TTL(Time-to-Live) 값은 6시간에서 90일 사이입니다. AuthN 토큰 만료는 자동으로 AuthZ 토큰 만료를 강제합니다. 인증 토큰의 TTL 값은 일반적으로 24시간입니다.

| 서버측 이벤트가 트리거됨 | <ul><li>인증 시도, 인증 보류 중, 인증 허용됨</li><li>인증 시도, 권한 부여됨</li><li>재생 요청 성공</li></ul> |
|---|---|


### 사용자 반환 - AuthZ 및 AuthN 토큰이 캐시됨

유효한 AuthZ 및 AuthN 토큰이 캐시된 사용자의 경우 다음 단계가 발생합니다.


![](assets/ae-flow-tokens-cached-web.png)



호출 시 자동으로 트리거됩니다. `getAuthorization()`에는 Adobe Primetime 인증을 사용하는 검사만 포함됩니다. MVPD는 이 흐름에 관여하지 않습니다.


| 서버측 이벤트가 트리거됨 | * 성공한 재생 요청 |
|---|---|


### 사용자 반환 - AuthN 토큰이 캐시됨, AuthZ 토큰이 만료됨

여전히 유효한 AuthN 토큰이 있는 사용자의 경우 다음 단계가 발생합니다.

![](assets/ae-flow-authn-token-cached.png)


이 흐름은 MVPD로의 왕복과 관련되어 있다.


| 서버측 이벤트가 트리거됨 | <ul><li>인증 시도, 인증 확인</li><li>재생 요청 성공</li> |
|---|---|

## 인증 이벤트 {#authn_events}

### 인증 시도 {#authentication-attempt}

위의 다이어그램에 표시된 것처럼, 인증 이벤트는 사용자가 MVPD로 왕복할 때만 트리거되며, 인증 이벤트는 캐시된 토큰 인증을 포함하지 않습니다.

인증 시도 이벤트는 사용자가 선택기에서 특정 MVPD를 클릭한 후 트리거됩니다.

* 이에 가까운 MVPD측의 첫 번째 이벤트는 페이지 로드입니다
* Adobe Primetime 인증은 사용자가 MVPD 페이지에 로그인하기 위해 반복적으로 시도한 횟수는 계산하지 않습니다(잘못된 암호, 다시 시도)
* 여러 번 시도하면 한 번의 시도로 계산됩니다
* 또한 일부 MVPD는 인증 단계에서 인증을 수행하고 인증에 실패하면 사용자가 다시 리디렉션되지 않습니다.

### 인증 보류 중 {#authentication-pending}

이 이벤트는 Adobe Primetime 인증으로의 리디렉션 프로세스가 시작될 때 발생합니다.

### 인증 부여됨 {#authentication-granted}

사용자는 MVPD의 알려진 구독자이며, 일반적으로 유료 TV 구독이 있지만, 경우에 따라 인터넷 액세스만 있습니다. 사용자가 MVPD로 유효한 자격 증명을 명시적으로 입력했거나, 이전에 유효한 자격 증명을 입력하고 &quot;내 정보 저장&quot;을 검사했기 때문에(그리고 이전 세션이 만료되지 않았기 때문에) 성공적인 인증이 발생할 수 있습니다.

따라서 MVPD는 Adobe Primetime 인증을 인증 요청에 대한 양의 응답을 보내고 Adobe Primetime 인증은 다음을 생성합니다. *AuthN 토큰*.

* 인증은 일반적으로 오랜 기간(한 달 이상) 동안 캐시됩니다. 이로 인해 토큰이 만료되고 흐름이 다시 시작될 때까지 인증 이벤트가 더 이상 표시되지 않습니다.
* SSO(Single Sign On)를 통해 다른 사이트/앱에서 들어오는 것은 인증 이벤트를 트리거하지 않습니다.



### Comcast 인증 {#comcast-authentication}

Comcast는 나머지 MVPD와 비교하여 다른 AuthN 흐름을 가지고 있습니다.

다음 기능은 그 차이점을 설명합니다.

* **세션 쿠키 동작**: 사용자가 브라우저를 닫은 후에 모든 인증 토큰이 완전히 제거됩니다. 이 기능은 웹에서만 사용할 수 있습니다. 주요 목적은 Comcast 세션이 안전하지 않은/공유 컴퓨터에서 지속되지 않도록 하는 것입니다. 그 영향은 나머지 MVPD에 비해 더 많은 인증 시도/부여 흐름이 있다는 것입니다.

* **요청자 ID당 AuthN**: Comcast에서 AuthN 상태를 한 요청자 ID에서 다른 요청자 ID로 캐시할 수 없습니다. 이로 인해 각 사이트/앱은 인증 토큰을 얻기 위해 Comcast로 이동해야 합니다. 사용자 경험 고려 사항 외에 위와 같은 영향은 더 많은 인증 시도/승인된 이벤트가 생성된다는 것입니다.

* **수동 인증**: 사용자 경험을 개선하면서도 요청자 ID별 AuthN 기능을 유지하기 위해 숨겨진 iFrame에서 수동 인증 흐름이 발생합니다. 사용자에게 아무것도 표시되지 않지만 이전처럼 이벤트가 계속 트리거됩니다.

사용자가 Comcast 로그인 페이지에서 &quot;내 정보 저장&quot;을 클릭하면 이후 이 페이지 방문(2주 이내)이 바로 리디렉션되어 돌아갑니다. 그렇지 않으면 사용자가 페이지에서 실제로 인증해야 합니다.

### 인증 실패 {#unsuccessful-authentication}

실패한 인증은 Adobe Primetime 인증에서 이벤트 자체가 아니지만 시도와 성공 간의 차이로 계산될 수 있습니다.

2013년 5월 릴리스에서는 Adobe Primetime 인증이 DRM 오류(토큰 바인딩 실패) 및 LSO 오류(토큰을 쓸 공간 없음 등)를 포함하여 시스템 또는 네트워크 오류로 인해 실패한 인증에 대한 오류 코드를 추가합니다.

### 인증 전환율 {#authenitication-conversion-rate}

프로그래머가 추적할 수 있는 한 가지 흥미로운 지표는 (AuthN 요청 / AuthN 부여됨)%로 계산된 인증 전환율입니다.

지표에 대한 일부 참고 사항:

* 이벤트 기반 지표이므로 고유한 사용자 전환율을 반영하지 않습니다. 사용자가 8번 시도하고 9번 성공한 경우 위의 전환율이 매우 나쁘게 반영됩니다.
* Adobe Primetime 인증(서버측)에서는 고유한 기반 인증 변환을 계산할 수 있는 방법이 없습니다.
* 사이트/앱에 자동 AuthN 재시도 가 있는 경우 위의 지표도 왜곡될 수 있습니다.

## 인증 이벤트 {#authorization_events}

### 인증 시도 {#authorization_attempt}

인증 토큰을 가져오는 것 외에도 사용자는 콘텐츠를 재생하기 전에 인증 토큰도 가져와야 합니다. 이 문제는 일반적으로 인증 후 또는 인증 토큰이 만료된 경우에 발생합니다. 이 검사는 서버측에서 수행되므로(Adobe Primetime 인증 서버에서 MVPD 서버로) 사용자는 아무 작업도 수행할 필요가 없습니다.

### 권한 부여됨 {#authorization-granted}

&quot;권한 부여&quot;는 인증된 사용자의 구독에 요청된 프로그래밍이 포함되어 있음을 나타냅니다.

일부 인증의 경우 권한 부여와 동일시되므로 일부 MVPD가 별도의 권한 부여 단계를 지원하는 것은 아닙니다. MVPD는 Adobe Primetime 인증을 백채널 AuthZ 요청에 대한 성공적인 응답을 보내고, Adobe Primetime 인증은 AuthZ 토큰을 만듭니다.

* AuthZ 토큰은 일정 기간 동안 캐시됩니다(일반적으로 24시간) 이 기간 동안에는 AuthZ 이벤트가 실행되지 않습니다.
* 일부 MVPD는 자산 수준 승인과 함께 작동하며, 다른 MVPD는 채널 수준 승인과 함께 작동합니다. - 어떤 MVPD를 사용하는지에 따라 AuthZ 이벤트가 실행되기도 합니다. 채널 수준 인증의 경우에도 캐싱이 적용됩니다. 따라서 24시간 이내에 동일한 에셋을 요청하면 이벤트가 실행되지 않습니다.

### 인증 거부됨 {#authorization-denied}

승인이 거부되면 인증된 사용자는 요청된 프로그래밍에 대해 확정된 구독을 보유하지 않습니다. 가장 가능성 있는 원인은 채널이 사용자의 구독 패키지의 일부가 아니지만, 이는 MVPD에서 인터넷 액세스만 갖는 사용자를 반영할 수도 있습니다.

일부 MVPD의 경우, 사용자는 MVPD의 인터넷 가입만 있어도(유료 TV 가입 없음) 성공적으로 인증됩니다. 이 경우 사용자가 권한 부여를 요청하는 채널이 기본 패키지에 있더라도 권한 부여가 거부됩니다.

일부 MVPD는 패키지를 업그레이드하는 오퍼를 포함할 수 있는 AuthZ 거부에 대한 사용자 지정 오류 메시지를 제공합니다.


### 인증 전환율 {#authorization-conversion-rate}

인증 전환율은 (AuthZ 요청 / AuthZ granted)%로 계산할 수 있습니다.

### 재생 요청 성공 {#successful-play-request}

인증된 사용자와 승인된 사용자는 보호된 콘텐츠를 볼 수 있습니다.

성공적인 재생 요청 시, Adobe Primetime 인증은 사용자가 요청된 비디오를 볼 자격이 있음을 나타내는 단기 미디어 토큰을 생성합니다. 프로그래머는 예상 뷰어의 추가 유효성 검사를 위해 이 미디어 토큰을 사용합니다. 미디어 토큰은 성공적인 재생 요청으로 추적됩니다.

* Adobe Primetime 인증은 *아님* 미디어 토큰을 생성한 후 비디오 재생이 실제로 시작되었는지 추적합니다. 예를 들어 콘텐츠에 지역 제한이 있는 경우 스트림이 실제로 시작되지 않더라도 트랜잭션은 여전히 성공적인 재생 요청으로 계산됩니다.
* AuthN 및 AuthZ 토큰은 일정 기간 동안 MVPD 응답을 캐시하므로, 성공적인 재생 요청 이벤트는 지표에서 가장 빈번한 이벤트이다.

## 고유 사용자 {#unique-users}

### 정의 {#definition}

인증에 성공하면 Adobe Primetime 인증은 반환된 MVPD 사용자 ID 값을 기반으로 고유 사용자의 존재를 추적합니다.  이 값은 사용자의 로그인 정보를 기반으로 하지만 개인 식별이 가능한 정보는 포함하지 않습니다.

이 값은 sendTrackingData 콜백의 사이트/앱에도 전달됩니다.

이 값은 장치 간에 지속적이거나(MVPD는 로그인이 발생하는 위치에 관계없이 지정된 사용자에 대해 동일한 값을 생성합니다.) 과도적이거나(각 로그인에 대해 MVPD가 백 엔드에 매핑하는 새 값이 생성됩니다.) 일반적으로 MVPD에서 Adobe Primetime 인증에 제공하는 값은 세션 및 장치 간에 지속되지만, 언급된 바와 같이 지속성이 보장되거나 검증되지 않습니다.

이 값은 고유 사용자를 계산하는 방법으로 사용됩니다. (요청자 ID/간격/MVPD당) 보고된 값이 특정 간격에 대해 중복 제거됩니다. 따라서 일일 고유 사용자의 합계는 일반적으로 월별 값과 다르며 월별 값은 더 낮은 값을 갖습니다.

이 숫자에는 Adobe Primetime 인증의 모든 이벤트에서 사용자 ID가 없는 인증 시도는 제외하지만 인증이 시도되었거나 실패할 수 있는 경우는 포함합니다.

### 예 {#examples}

#### 1일 {#day1}

사용자 XYZ는 비디오를 보기 위해 사이트로 이동합니다.

실행된 이벤트:

* AuthN 시도(아직 고유 사용자 없음)
* AuthN 부여
   * 이 시점에서 MVPD가 반환하는 것을 기반으로 사용자를 고유하게 식별하므로 일일 고유 사용자 수가 1씩 증가합니다
   * authN 토큰이 30일 동안 캐시됨
* AuthZ 시도/부여 이벤트
   * 1일 동안 캐시된 AuthZ 토큰
* 재생 요청 이벤트 성공

#### 1일(나중에) {#day1-later-on}

사용자 XYZ는 다른 비디오를 시청합니다.

실행된 이벤트:

* 재생 요청 이벤트 성공(나머지는 캐시됨)
* 일별 또는 월별 고유 수 증가 없음

#### 3일 {#day3}

사용자 XYZ는 다른 비디오를 시청합니다.

실행된 이벤트:

* AuthZ 시도/부여 이벤트
   * 1일의 1일 캐싱이 만료되었으므로
* 재생 요청 이벤트 성공(나머지는 캐시됨)
* 일별 고유 사용자 수 1 증가 - 월별 고유 수 여전히 1

#### 31일 {#day31}

사용자 XYZ는 다른 비디오를 시청합니다.

AuthN 캐싱이 만료된 이후 1일과 동일합니다.

동일한 사용자가 인증에 실패한 경우 사용자 ID가 포함된 두 개의 이벤트(인증 부여 및 권한 부여 시도)가 있으므로 월별 고유 사용자 수가 여전히 1명 증가합니다.

### SSO(단일 인증) {#single-sign-on-sso}

일부 경우들에서, 고유 사용자들의 수는 성공적인 인증들의 수보다 클 수 있다. 일반적으로 많은 사용자가 다른 사이트/앱에서 SSO를 통해 들어오는 경우에 해당되며 현재 사이트/앱에 대한 인증만 받으면 됩니다.

### 클라이언트측 고유 사용자와 서버측 고유 사용자 비교 {#comparing-client-side-and-server-side-unique-users}

의 사용자 ID 값인 경우 `sendTrackingData()` 는 클라이언트측에서 고유 사용자를 카운트하는 데 사용되며 클라이언트측과 서버측 번호는 일치해야 합니다.

차이가 큰 경우 일반적으로 다음 이유로 차이가 발생합니다.

* 비디오 재생 고유 대 모든 이벤트 고유. 앞에서 언급했듯이 Adobe Primetime 인증은 AuthN 시도를 제외한 모든 이벤트에 대해 고유 사용자를 계산합니다. 즉, 사용자가 (페이지에서) 인증만 하고 비디오를 보지 않는 경우 고유한 사용자 수 증가가 계속 트리거됩니다.

* 권한 부여에 실패한 사용자 수 계산 - Adobe Primetime 인증은 보고된 수에서도 이러한 사용자를 계산합니다.

<!--
## Related Information {#related-information}

- [Entitlement Service Monitoring API](/help/authentication/entitlement-service-monitoring-api.md)

-->
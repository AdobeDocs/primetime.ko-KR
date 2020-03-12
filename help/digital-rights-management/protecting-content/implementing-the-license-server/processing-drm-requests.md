---
seo-title: Adobe Primetime DRM 요청 처리
title: Adobe Primetime DRM 요청 처리
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Adobe Primetime DRM 요청 처리 {#process-adobe-primetime-drm-requests}

요청을 관리하는 일반적인 방법은 핸들러를 만들고, 요청을 구문 분석하고, 응답 데이터 또는 오류 코드를 설정하고, 핸들러를 닫는 것입니다.

단일 요청/응답 상호 작용을 처리하는 데 사용되는 기본 클래스는 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`입니다. 클래스의 인스턴스는 `HandlerConfiguration` 처리기를 초기화하는 데 사용됩니다. `HandlerConfiguration` 전송 자격 증명, 타임스탬프 허용치, 정책 업데이트 목록 및 해지 목록을 포함한 서버 구성 정보를 저장합니다. 이 처리기는 요청 데이터를 읽고 요청을 `RequestMessageBase`의 인스턴스로 구문 분석합니다. 호출자는 요청에 있는 정보를 검사하고 오류를 반환할지 또는 성공적인 응답을 결정할 수 있습니다(의 하위 클래스는 응답 데이터를 설정하는 방법을 `RequestMessageBase` 제공합니다).

요청이 성공하면 응답 데이터를 설정합니다.그렇지 않으면 실패 시 `RequestMessageBase.setErrorData()` 호출할 수 있습니다. 항상 메서드를 호출하여 구현을 종료합니다( `close()` 문의 `close()` 블록에서 `finally` `try` 호출하는 것이 좋습니다.). 핸들러를 호출하는 `MessageHandlerBase` 방법의 예는 API 참조 설명서를 참조하십시오.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>HTTP 상태 코드 200(확인)은 처리기에서 처리하는 모든 요청에 응답하여 전송해야 합니다. 서버 오류로 인해 처리기를 만들 수 없는 경우 서버가 500(내부 서버 오류)과 같은 다른 상태 코드로 응답할 수 있습니다.

클라이언트는 패키징 시 지정된 라이센스 서버 URL을 라이센스 서버로 전송된 모든 요청에 대한 기본 URL로 사용합니다. 예를 들어, 서버 URL이 &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>으로 지정된 경우 클라이언트는 &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]> 각 요청 유형에 사용되는 특정 경로에 대한 자세한 내용은 다음 섹션을 참조하십시오. 라이센스 서버를 구현할 때는 서버가 각 요청 유형에 필요한 경로에 응답해야 합니다.

라이센스 요청에는 인증 토큰이 포함될 수 있습니다. 사용자 이름/암호 인증이 사용된 경우, 요청에 에서 `AuthenticationToken` 생성한 항목이 포함될 수 `AuthenticationHandler`있으며, SDK는 라이센스를 발급하기 전에 토큰이 유효한지 확인합니다.

## 컴퓨터 식별자 사용 {#use-machine-identifiers}

모든 Adobe Primetime DRM 요청(FMRMS 호환성을 지원하는 요청 제외)에는 개인화 동안 클라이언트에 발급된 컴퓨터 토큰에 대한 정보가 포함됩니다. 컴퓨터 토큰에는 개인화 중에 할당된 식별자인 컴퓨터 ID가 포함됩니다. 이 식별자를 사용하여 사용자가 라이센스를 요청했거나 도메인에 가입한 시스템의 수를 계산할 수 있습니다.

식별자를 다음과 같이 사용할 수 있습니다.

* 이 `getUniqueId()` 메서드는 개별화 중에 장치에 지정된 문자열을 반환합니다. 데이터베이스에 문자열을 저장하고 식별자별로 검색할 수 있습니다. 그러나 이 식별자는 사용자가 하드 드라이브를 다시 포맷하고 다시 식별하면 변경됩니다. 또한 이 식별자는 동일한 시스템의 서로 다른 브라우저에서 Adobe AIR와 Adobe Flash Player 간에 다른 값을 갖습니다.
* 컴퓨터를 보다 정확하게 계산하려면 전체 식별자를 저장하는 `getBytes()` 데 사용할 수 있습니다. 시스템이 이전에 표시되었는지 확인하려면 사용자 이름에 대한 모든 식별자를 가져와서 일치하는지 `matches()` 확인합니다. 이 `matches()` 방법은 에서 반환되는 값을 비교하는 데 사용해야 하므로 이 `MachineId.getBytes`옵션은 비교할 값이 적은 경우에만 실용적입니다.예를 들어, 특정 사용자와 연결된 컴퓨터가 있습니다.

## 사용자 인증 {#user-authentication}

Adobe Primetime DRM 요청에는 인증 토큰이 포함될 수 있습니다.

사용자 이름/암호 인증이 사용된 경우, 요청에는 에서 `AuthenticationToken` 생성된 ID가 포함될 수 `AuthenticationHandler`있습니다. 토큰에 액세스하여 확인하려면 반드시 사용해야 합니다 `RequestMessageBase.getAuthenticationToken()`. 클라이언트에서 사용자 이름/암호 요청을 시작하려면 ActionScript 또는 iOS API를 `DRMManager.authenticate()` 사용합니다.

클라이언트와 서버가 사용자 정의 인증 메커니즘을 사용하는 경우 클라이언트는 다른 채널을 통해 인증 토큰을 입수하고 ActionScript 3.0 API를 사용하여 사용자 정의 인증 토큰을 `DRMManager.setAuthenticationToken` 설정합니다. 사용자 정의 인증 토큰을 `RequestMessageBase.getRawAuthenticationToken()` 가져오는 데 사용합니다. 서버 구현은 사용자 정의 인증 토큰이 유효한지 여부를 결정합니다.

## 재생 보호 {#replay-protection}

재생 보호를 위해, 전화를 통해 메시지 식별자가 최근에 표시되었는지 확인할 수 `RequestMessageBase.getMessageId()`있습니다. 이러한 경우, 침입자가 요청을 다시 재생하려고 할 수 있으며 이는 거부되어야 합니다. 재생 시도를 감지하기 위해 서버는 최근에 본 메시지 ID 목록을 저장하고 캐시된 목록에 대해 들어오는 각 요청을 확인할 수 있습니다. 메시지 식별자를 저장해야 하는 시간을 제한하려면 을 호출하십시오. `HandlerConfiguration.setTimestampTolerance()` 이 속성을 설정하면 SDK는 지정된 시간(초) 이상 타임스탬프를 포함하는 요청을 거부합니다.

## 롤백 감지 {#rollback-detection}

롤백 감지의 경우 일부 사용 규칙은 클라이언트가 권한 적용을 위해 상태 정보를 유지해야 합니다. 예를 들어, 재생 창 사용 규칙을 적용하기 위해 클라이언트는 사용자가 처음 컨텐츠를 보기 시작한 날짜와 시간을 저장합니다. 이 이벤트는 재생 창의 시작을 트리거합니다. 재생 창을 안전하게 적용하려면 서버에서 사용자가 클라이언트 상태를 백업 및 복원하지 않고 클라이언트에 저장된 재생 창 시작 시간을 제거해야 합니다. 서버는 클라이언트의 롤백 카운터 값을 추적하여 이 작업을 수행합니다.

각 요청에 대해 서버는 `RequestMessageBase.getClientState()` 객체를 가져오기 `ClientState` 위해 호출한 다음 클라이언트 상태 카운터의 현재 값을 가져오기 `ClientState.getCounter()` 위해 호출하여 카운터의 값을 가져옵니다. 서버는 각 클라이언트에 대해 이 값을 저장하고(롤백 카운터 값과 연결된 클라이언트를 `MachineId.getUniqueId()` 식별하는 데 사용), 카운터 값을 하나씩 `ClientState.incrementCounter()` 늘리도록 호출해야 합니다. 서버가 카운터 값이 서버에서 마지막으로 본 값보다 작음을 감지하면 클라이언트 상태가 롤백되었을 수 있습니다.

클라이언트 상태 `ClientState` 변조 감지에 대한 자세한 내용은 API 참조 설명서를 참조하십시오.

## 전역 서버 구성 데이터{#global-server-configuration-data}

라이센스 서버에서 사용하는 구성 외에도 `HandlerConfiguration` 클라이언트에 전송하여 라이센스가 적용되는 방식을 제어할 수 있는 구성 정보를 저장합니다. 이 작업은 `ServerConfigData` 클래스를 만들고 호출을 통해 수행됩니다 `HandlerConfiguration.setServerConfigData()`. 이러한 설정은 이 라이선스 서버에서 발급한 라이선스에만 적용됩니다.

클럭 윈드백 허용치는 클라이언트가 라이센스를 적용하는 방법을 제어하기 위해 라이센스 서버에서 설정할 수 있는 하나의 속성입니다. 기본적으로 사용자는 라이선스를 무효화하지 않고 시스템 시계를 4시간 뒤로 설정할 수 있습니다. 라이선스 서버 운영자가 다른 설정을 사용하려면 `ServerConfigData` 클래스에서 새 값을 설정할 수 있습니다. 이러한 설정의 값을 변경할 때는 반드시 호출함으로써 버전 번호를 증가시켜야 `setVersion()`합니다. 새 값은 클라이언트의 버전이 현재 `ServerConfigData` 버전보다 오래된 경우에만 클라이언트에 전송됩니다.

## 크로스 도메인 DRM 정책 파일 {#crossdomain-drm-policy-file}

라이센스 서버가 비디오 재생 SWF가 아닌 다른 도메인에 호스팅되는 경우 SWF가 라이센스 서버에서 라이센스를 요청하도록 하는 크로스 도메인 DRM 정책 파일( [!DNL crossdomain.xml])이 필요합니다. 크로스 도메인 DRM 정책 파일은 XML 파일로 표현되므로 서버에서 다른 도메인에서 제공되는 SWF 파일에 데이터와 문서를 사용할 수 있음을 나타냅니다. 라이선스 서버의 크로스 도메인 DRM 정책 파일에 지정된 도메인에서 제공되는 모든 SWF 파일은 해당 라이선스 서버의 데이터 또는 에셋에 액세스할 수 있습니다.

Adobe에서는 개발자가 트러스트된 도메인만 라이센스 서버에 액세스하고 웹 서버의 라이센스 하위 디렉토리에 대한 액세스를 제한하여 크로스 도메인 정책 파일을 배포할 때 모범 사례를 따를 것을 권장합니다.

크로스 도메인 DRM 정책 파일에 대한 자세한 내용은 다음 위치를 참조하십시오.

* 웹 사이트 컨트롤(DRM 정책 파일)
* 크로스 도메인 DRM 정책 파일 사양: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
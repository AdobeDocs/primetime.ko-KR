---
seo-title: Adobe Primetime DRM 요청 처리
title: Adobe Primetime DRM 요청 처리
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# 프로세스 Adobe Primetime DRM 요청 {#process-adobe-primetime-drm-requests}

요청을 관리하는 일반적인 방법은 핸들러를 만들고, 요청을 구문 분석하고, 응답 데이터 또는 오류 코드를 설정하고, 핸들러를 닫는 것입니다.

단일 요청/응답 상호 작용을 처리하는 데 사용되는 기본 클래스는 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`입니다. `HandlerConfiguration` 클래스의 인스턴스가 핸들러를 초기화하는 데 사용됩니다. `HandlerConfiguration` 전송 자격 증명, 타임스탬프 허용 한도, 정책 업데이트 목록 및 해지 목록을 포함한 서버 구성 정보를 저장합니다.이 처리기는 요청 데이터를 읽고 요청을 한 인스턴스에 구문 분석합니다 `RequestMessageBase`. 호출자는 요청의 정보를 검사하고 오류를 반환할지 또는 성공적인 응답을 반환할지 결정할 수 있습니다(`RequestMessageBase`의 하위 클래스는 응답 데이터를 설정하는 방법을 제공합니다).

요청이 성공하면 응답 데이터를 설정합니다.그렇지 않으면 실패 시 `RequestMessageBase.setErrorData()`을(를) 불러옵니다. 항상 `close()` 메서드를 호출하여 구현을 종료합니다.(`try` 문의 `finally` 블록에서 `close()`을 호출하는 것이 좋습니다.) 핸들러를 호출하는 방법의 예는 `MessageHandlerBase` API 참조 설명서를 참조하십시오.

>[!NOTE]
>
>HTTP 상태 코드 200(OK)은 처리기에서 처리하는 모든 요청에 응답하여 전송되어야 합니다. 서버 오류로 인해 핸들러를 만들 수 없는 경우 서버가 500(내부 서버 오류)과 같은 다른 상태 코드로 응답할 수 있습니다.

클라이언트는 패키지 시간에 지정된 라이센스 서버 URL을 라이센스 서버에 전송된 모든 요청에 대한 기본 URL로 사용합니다. 예를 들어 서버 URL이 &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>으로 지정된 경우 클라이언트는 &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...에 요청을 보냅니다.] 각 요청 유형에 사용되는 특정 경로에 대한 자세한 내용은 다음 섹션을 참조하십시오. 라이센스 서버를 구현할 때는 서버가 각 요청 유형에 필요한 경로에 응답해야 합니다.

라이센스 요청에는 인증 토큰이 포함될 수 있습니다. 사용자 이름/암호 인증이 사용된 경우 요청에 `AuthenticationHandler`에서 생성된 `AuthenticationToken`이 포함될 수 있으며 SDK는 라이선스를 발급하기 전에 토큰이 유효한지 확인합니다.

## 컴퓨터 식별자 {#use-machine-identifiers} 사용

모든 Adobe Primetime DRM 요청(FMRMS 호환성을 지원하는 요청 제외)에는 개인화 중 클라이언트에 발급된 컴퓨터 토큰에 대한 정보가 포함되어 있습니다. 컴퓨터 토큰에는 개인화 중에 할당된 식별자인 컴퓨터 ID가 포함됩니다. 이 식별자를 사용하여 사용자가 라이선스를 요청했거나 도메인에 가입한 시스템의 수를 계산할 수 있습니다.

식별자를 다음과 같이 사용할 수 있습니다.

* `getUniqueId()` 메서드는 개별화 중 장치에 지정된 문자열을 반환합니다. 데이터베이스에 문자열을 저장하고 식별자별로 검색할 수 있습니다. 그러나 이 식별자는 사용자가 하드 드라이브를 다시 포맷하고 다시 개인화할 경우 변경됩니다. 또한 이 식별자는 동일한 컴퓨터의 서로 다른 브라우저에 있는 Adobe AIR 및 Adobe Flash Player 간에 다른 값을 갖습니다.
* 컴퓨터를 더 정확히 계산하려면 `getBytes()`을 사용하여 전체 식별자를 저장할 수 있습니다. 시스템이 이전에 표시되었는지 확인하려면 사용자 이름에 대한 모든 식별자를 얻고 `matches()`을 호출하여 일치하는 항목이 있는지 확인합니다. `matches()` 메서드를 사용하여 `MachineId.getBytes`에서 반환된 값을 비교해야 하므로 이 옵션은 비교할 값이 적은 경우에만 실용적입니다.예를 들어, 특정 사용자와 연결된 시스템이 있습니다.

## 사용자 인증 {#user-authentication}

Adobe Primetime DRM 요청에는 인증 토큰이 포함될 수 있습니다.

사용자 이름/암호 인증이 사용된 경우 요청에는 `AuthenticationHandler`에서 생성된 `AuthenticationToken`이 포함될 수 있습니다. 토큰에 액세스하여 확인하려면 `RequestMessageBase.getAuthenticationToken()`을 사용해야 합니다. 클라이언트에서 사용자 이름/암호 요청을 시작하려면 `DRMManager.authenticate()` ActionScript 또는 iOS API를 사용하십시오.

클라이언트와 서버가 사용자 정의 인증 메커니즘을 사용하는 경우 클라이언트는 다른 채널을 통해 인증 토큰을 입수하고 `DRMManager.setAuthenticationToken` ActionScript 3.0 API를 사용하여 사용자 정의 인증 토큰을 설정합니다. `RequestMessageBase.getRawAuthenticationToken()`을(를) 사용하여 사용자 정의 인증 토큰을 가져옵니다. 서버 구현은 사용자 지정 인증 토큰이 유효한지 여부를 결정합니다.

## 보호 재생 {#replay-protection}

재생 보호를 위해 `RequestMessageBase.getMessageId()`을(를) 호출하여 메시지 식별자가 최근에 표시되었는지 확인할 수 있습니다. 이러한 경우 침입자가 요청을 다시 재생하려고 할 수 있으며 거부해야 합니다. 재생 시도를 감지하기 위해 서버는 최근에 본 메시지 ID 목록을 저장하고 캐시된 목록에 대해 들어오는 각 요청을 확인할 수 있습니다. 메시지 식별자를 저장해야 하는 시간을 제한하려면 `HandlerConfiguration.setTimestampTolerance()`을(를) 호출하십시오. 이 속성이 설정되면 SDK는 지정된 시간(초) 이상 타임스탬프를 전달하는 요청을 거부합니다.

## 롤백 감지 {#rollback-detection}

롤백 탐지의 경우 일부 사용 규칙은 클라이언트가 권한 적용을 위해 상태 정보를 유지해야 합니다. 예를 들어, 재생 창 사용 규칙을 적용하기 위해 클라이언트는 사용자가 처음 컨텐츠를 보기 시작한 날짜와 시간을 저장합니다. 이 이벤트는 재생 창의 시작을 트리거합니다. 재생 창을 안전하게 적용하려면 서버가 클라이언트 상태를 백업 및 복원하지 않고 클라이언트에 저장된 재생 창 시작 시간을 제거해야 합니다. 서버는 클라이언트의 롤백 카운터 값을 추적하여 이 작업을 수행합니다.

각 요청에 대해 서버는 `RequestMessageBase.getClientState()`을(를) 호출하여 `ClientState` 개체를 가져온 다음 `ClientState.getCounter()`를 호출하여 클라이언트 상태 카운터의 현재 값을 가져옵니다. 서버는 각 클라이언트에 대해 이 값을 저장해야 합니다(롤백 카운터 값과 연결된 클라이언트를 식별하려면 `MachineId.getUniqueId()` 사용). 그런 다음 `ClientState.incrementCounter()`을(를) 호출하여 카운터 값을 하나씩 증가시켜야 합니다. 서버가 카운터 값이 서버에서 마지막으로 본 값보다 작다는 것을 감지하면 클라이언트 상태가 롤백되었을 수 있습니다.

클라이언트 상태 변조 검색에 대한 자세한 내용은 `ClientState` API 참조 설명서를 참조하십시오.

## 전역 서버 구성 데이터{#global-server-configuration-data}

라이센스 서버에서 사용하는 구성 외에도 `HandlerConfiguration`은(는) 라이센스의 적용 방법을 제어하기 위해 클라이언트에 전송할 수 있는 구성 정보를 저장합니다. 이 작업은 `ServerConfigData` 클래스를 만들고 `HandlerConfiguration.setServerConfigData()`을(를) 호출하여 수행됩니다. 이러한 설정은 이 라이선스 서버에서 발급한 라이선스에만 적용됩니다.

클럭 윈드백 허용치는 클라이언트가 라이센스를 적용하는 방법을 제어하기 위해 라이센스 서버에서 설정할 수 있는 하나의 속성입니다. 기본적으로 사용자는 라이선스를 무효화하지 않고 시스템 클럭 4시간을 설정할 수 있습니다. 라이선스 서버 연산자가 다른 설정을 사용하려면 `ServerConfigData` 클래스에서 새 값을 설정할 수 있습니다. 이러한 설정의 값을 변경할 때는 `setVersion()`을(를) 호출하여 버전 번호를 증가시켜야 합니다. 새 값은 클라이언트의 버전이 현재 `ServerConfigData` 버전보다 오래된 경우에만 클라이언트에 전송됩니다.

## 크로스 도메인 DRM 정책 파일 {#crossdomain-drm-policy-file}

라이센스 서버가 비디오 재생 SWF와 다른 도메인에 호스팅되는 경우 SWF가 라이센스 서버의 라이센스를 요청하도록 하려면 크로스 도메인 DRM 정책 파일( [!DNL crossdomain.xml])이 필요합니다. 크로스 도메인 DRM 정책 파일은 다른 도메인에서 제공되는 SWF 파일에 해당 데이터와 문서를 사용할 수 있음을 나타내는 XML 파일로 표시됩니다. 라이선스 서버의 크로스 도메인 DRM 정책 파일에 지정된 도메인에서 제공되는 SWF 파일은 해당 라이선스 서버의 데이터 또는 에셋에 액세스할 수 있습니다.

Adobe은 개발자가 트러스트된 도메인만 라이센스 서버에 액세스하고 웹 서버의 라이센스 하위 디렉토리에 대한 액세스를 제한함으로써 크로스 도메인 정책 파일을 배포할 때 모범 사례를 따를 것을 권장합니다.

크로스 도메인 DRM 정책 파일에 대한 자세한 내용은 다음 위치를 참조하십시오.

* 웹 사이트 제어(DRM 정책 파일)
* 크로스 도메인 DRM 정책 파일 사양:[https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
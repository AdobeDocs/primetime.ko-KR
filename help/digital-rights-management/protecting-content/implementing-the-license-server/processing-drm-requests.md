---
title: Adobe Primetime DRM 요청 처리
description: Adobe Primetime DRM 요청 처리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# Adobe Primetime DRM 요청 처리 {#process-adobe-primetime-drm-requests}

요청을 관리하는 일반적인 방법은 핸들러를 만들고, 요청을 구문 분석하고, 응답 데이터 또는 오류 코드를 설정하고, 핸들러를 닫는 것입니다.

단일 요청/응답 상호 작용을 처리하는 데 사용되는 기본 클래스는 다음과 같습니다. `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. 의 인스턴스 `HandlerConfiguration` 클래스를 사용하여 처리기를 초기화할 수 있습니다. `HandlerConfiguration` 전송 자격 증명, 타임스탬프 허용 오차, 정책 업데이트 목록 및 해지 목록을 포함한 서버 구성 정보를 저장합니다. 처리기는 요청 데이터를 읽고 요청을 다음 인스턴스로 구문 분석합니다. `RequestMessageBase`. 호출자는 요청의 정보를 검사하고 오류 또는 성공적인 응답을 반환할지 여부를 결정할 수 있습니다(의 하위 클래스). `RequestMessageBase` 응답 데이터를 설정하는 방법을 제공합니다).

요청이 성공하면 응답 데이터를 설정하고, 그렇지 않으면 를 호출합니다. `RequestMessageBase.setErrorData()` 실패 시. 항상 를 호출하여 구현을 종료하십시오 `close()` 메서드(권장 사항) `close()` 호출될 위치: `finally` 블록 `try` 문)을 참조하십시오. 다음을 참조하십시오. `MessageHandlerBase` 처리기를 호출하는 방법의 예를 보려면 API 참조 설명서입니다.

>[!NOTE]
>
>HTTP 상태 코드 200(OK)은 핸들러가 처리한 모든 요청에 대한 응답으로 전송되어야 합니다. 서버 오류로 인해 핸들러를 만들 수 없는 경우 서버는 500(내부 서버 오류)과 같은 다른 상태 코드로 응답할 수 있습니다.

클라이언트는 패키징 시간에 지정된 라이선스 서버 URL을 라이선스 서버에 전송된 모든 요청에 대한 기본 URL로 사용합니다. 예를 들어 서버 URL이 &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>을(를) 입력하면 클라이언트가 &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]> 각 요청 유형에 사용되는 특정 경로에 대한 자세한 내용은 다음 섹션을 참조하십시오. 라이센스 서버를 구현할 때는 서버가 각 요청 유형에 필요한 경로에 응답해야 합니다.

라이선스 요청에는 인증 토큰이 포함될 수 있습니다. 사용자 이름/암호 인증을 사용한 경우 요청에 `AuthenticationToken` 생성된 사람 `AuthenticationHandler`를 입력하면 SDK는 라이선스를 발급하기 전에 토큰이 유효한지 확인합니다.

## 컴퓨터 식별자 사용 {#use-machine-identifiers}

모든 Adobe Primetime DRM 요청(FMRMS 호환성을 지원하는 요청 제외)에는 개별화 중에 클라이언트에 발급된 컴퓨터 토큰에 대한 정보가 포함됩니다. 머신 토큰은 개별화 동안 할당된 식별자인 머신 ID를 포함한다. 이 식별자를 사용하여 사용자가 라이선스를 요청하거나 도메인에 가입한 컴퓨터 수를 계산할 수 있습니다.

식별자는 다음과 같이 사용할 수 있습니다.

* 다음 `getUniqueId()` 메서드는 개별화 중에 디바이스에 할당된 문자열을 반환합니다. 데이터베이스에 문자열을 저장하고 식별자로 검색할 수 있습니다. 그러나 사용자가 하드 드라이브를 다시 포맷하고 다시 개인화하면 이 식별자가 변경됩니다. 또한 이 식별자는 동일한 컴퓨터의 다른 브라우저에서 Adobe AIR과 Adobe Flash Player 간에 다른 값을 갖습니다.
* 컴퓨터를 보다 정확하게 계산하려면 다음을 사용할 수 있습니다. `getBytes()` 전체 식별자를 저장합니다. 컴퓨터가 이전에 표시되었는지 확인하려면 사용자 이름과 호출에 대한 모든 식별자를 가져옵니다 `matches()` 일치하는 항목이 있는지 확인합니다. 이유: `matches()` 메서드는에서 반환한 값을 비교하는 데 사용해야 합니다. `MachineId.getBytes`, 이 옵션은 비교할 값이 적은 경우(예: 특정 사용자와 연관된 컴퓨터)에만 실용적입니다.

## 사용자 인증 {#user-authentication}

Adobe Primetime DRM 요청은 인증 토큰을 포함할 수 있습니다.

사용자 이름/암호 인증이 사용된 경우 요청에 `AuthenticationToken` 생성된 사람 `AuthenticationHandler`. 토큰에 액세스하고 확인하려면 다음을 사용해야 합니다. `RequestMessageBase.getAuthenticationToken()`. 클라이언트에서 사용자 이름/암호 요청을 시작하려면 `DRMManager.authenticate()` ActionScript 또는 iOS API입니다.

클라이언트와 서버가 사용자 지정 인증 메커니즘을 사용하는 경우 클라이언트는 다른 채널을 통해 인증 토큰을 획득하고 다음을 사용하여 사용자 지정 인증 토큰을 설정합니다. `DRMManager.setAuthenticationToken` ActionScript 3.0 API입니다. 사용 `RequestMessageBase.getRawAuthenticationToken()` 사용자 지정 인증 토큰을 가져옵니다. 서버 구현은 사용자 지정 인증 토큰이 유효한지 여부를 결정합니다.

## 재생 보호 {#replay-protection}

재생 보호의 경우 를 호출하여 메시지 식별자가 최근에 표시되었는지 확인할 수 있습니다. `RequestMessageBase.getMessageId()`. 그런 경우 공격자가 요청을 재생하려고 할 수 있으며 이는 거부되어야 합니다. 재생 시도를 검출하기 위해, 서버는 최근에 본 메시지 ID의 목록을 저장하고, 캐싱된 목록에 대해 각각의 수신 요청을 검사할 수 있다. 메시지 식별자를 저장해야 하는 시간을 제한하려면 을 호출하십시오. `HandlerConfiguration.setTimestampTolerance()`. 이 속성이 설정되면 SDK는 지정된 서버 시간(초) 이상 동안 타임스탬프를 전달하는 모든 요청을 거부합니다.

## 롤백 감지 {#rollback-detection}

롤백 감지를 위해 일부 사용 규칙은 클라이언트가 권한을 시행하기 위해 상태 정보를 유지 관리해야 합니다. 예를 들어 재생 창 사용 규칙을 적용하기 위해 클라이언트는 사용자가 콘텐츠를 처음 보기 시작한 날짜 및 시간을 저장합니다. 이 이벤트는 재생 창의 시작을 트리거합니다. 재생 창을 안전하게 적용하려면 서버에서 사용자가 클라이언트 상태를 백업 및 복원하지 않도록 하여 클라이언트에 저장된 재생 창 시작 시간을 제거해야 합니다. 서버는 클라이언트의 롤백 카운터 값을 추적하여 이를 수행합니다.

각 요청에 대해 서버는 를 호출하여 카운터 값을 가져옵니다. `RequestMessageBase.getClientState()` 을(를) 가져오려면 `ClientState` 객체, 호출 `ClientState.getCounter()` 클라이언트 상태 카운터의 현재 값을 가져옵니다. 서버는 각 클라이언트에 대해 이 값을 저장해야 합니다(사용 `MachineId.getUniqueId()` 를 눌러 롤백 카운터 값)과 연관된 클라이언트를 식별한 다음 `ClientState.incrementCounter()` 카운터 값을 1씩 늘립니다. 서버가 카운터 값이 서버에서 확인한 마지막 값보다 작음을 감지하면 클라이언트 상태가 롤백되었을 수 있습니다.

다음을 참조하십시오. `ClientState` 클라이언트 상태 변조 탐지에 대한 자세한 내용은 API 참조 설명서 를 참조하십시오.

## 전역 서버 구성 데이터{#global-server-configuration-data}

라이센스 서버에서 사용하는 구성 외에도 `HandlerConfiguration` 는 라이선스가 적용되는 방식을 제어하기 위해 클라이언트에 보낼 수 있는 구성 정보를 저장합니다. 이 작업은 다음을 생성하여 수행합니다 `ServerConfigData` 클래스 및 호출 `HandlerConfiguration.setServerConfigData()`. 이 설정은 이 라이선스 서버에서 발급한 라이선스에만 적용됩니다.

클럭 윈드백 허용 오차는 클라이언트가 라이선스를 집행하는 방법을 제어하기 위해 라이선스 서버에서 설정할 수 있는 속성 중 하나입니다. 기본적으로 사용자는 라이센스를 무효화하지 않고 기계 시계를 4시간 뒤로 설정할 수 있습니다. 라이센스 서버 운영자가 다른 설정을 사용하려는 경우 새 값을 `ServerConfigData` 클래스. 이러한 설정의 값을 변경할 때는 를 호출하여 버전 번호를 증가시켜야 합니다 `setVersion()`. 클라이언트의 버전이 현재 버전보다 오래된 경우에만 새 값이 클라이언트에 전송됩니다 `ServerConfigData` 버전.

## 교차 도메인 DRM 정책 파일 {#crossdomain-drm-policy-file}

라이센스 서버가 비디오 재생 SWF과 다른 도메인에서 호스팅되는 경우 도메인 간 DRM 정책 파일( [!DNL crossdomain.xml])는 SWF이 라이선스 서버에서 라이선스를 요청할 수 있도록 하는 데 필요합니다. 도메인 간 DRM 정책 파일은 서버에서 다른 도메인에서 제공되는 SWF 파일에 해당 데이터와 문서를 사용할 수 있음을 나타내는 XML 파일로 표시됩니다. 라이센스 서버의 도메인 간 DRM SWF 파일에 지정된 도메인에서 제공되는 모든 정책 파일은 해당 라이센스 서버의 데이터 또는 에셋에 액세스할 수 있습니다.

Adobe은 개발자가 도메인 간 정책 파일을 배포할 때 신뢰할 수 있는 도메인만 라이선스 서버에 액세스하도록 허용하고 웹 서버의 라이선스 하위 디렉터리에 대한 액세스를 제한하여 모범 사례를 따를 것을 권장합니다.

도메인 간 DRM 정책 파일에 대한 자세한 내용은 다음 위치를 참조하십시오.

* 웹 사이트 컨트롤(DRM 정책 파일)
* 도메인 간 DRM 정책 파일 사양: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

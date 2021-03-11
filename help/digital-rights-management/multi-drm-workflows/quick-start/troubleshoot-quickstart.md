---
description: 테스트 중에 일반적인 문제는 ExpressPlay 인증, 전송 프로토콜 및 필요한 서비스 요청 매개 변수와 관련된 경우가 많습니다.
title: 빠른 시작 문제 해결
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# 빠른 시작 문제 해결{#troubleshooting-your-quick-start}

테스트 중에 일반적인 문제는 ExpressPlay 인증, 전송 프로토콜 및 필요한 서비스 요청 매개 변수와 관련된 경우가 많습니다.

토큰 생성을 위해 [!DNL curl] ExpressPlay에 대한 요청이 실패한 경우 응답 본문에 실패 이유를 설명하는 오류 메시지가 포함됩니다.

토큰 생성에 성공했지만 내용이 여전히 재생되지 않는 경우 ExpressPlay 토큰 상환 로그에서 &quot;만료된 토큰&quot;과 같은 오류를 확인하십시오.

토큰 생성에 성공했고 상환에 오류가 없지만 비디오가 여전히 재생되지 않으면 CEK가 내용과 일치하는지, 내용 형식이 대상 장치의 기능과 일치하는지 확인합니다.

추가:

* 서비스 요청에서 올바른 고객 인증자를 사용하고 있는지 확인하십시오. 테스트 인증자를 사용하려는 경우 제작 인증자를 실수로 사용하는 것이 쉽습니다. 또한 *your* 인증자를 사용하고 있는지 확인하십시오. 예를 들어 테스트 중에 다른 사람의 `curl` 명령을 빌리고 인증자를 다른 사람의 인증자로 바꾸는 것을 잊어버릴 수 있습니다.

* 요청이나 매니페스트에 적절한 전송 프로토콜을 사용하고 있는지 확인하십시오( `https://` 대 `https://`) 또는 FairPlay의 경우 `https://` 대 `https://``skd://`

* 작업 중인 DRM 솔루션에 필요한 모든 쿼리 매개 변수를 포함해야 합니다. 예를 들어 PlayReady와 Widevine을 혼돈하는 것은 쉽습니다. PlayReady는 DASH로 작동하지만 필요한 요청 매개 변수와 패키징 구성은 다릅니다.
* ExpressPlay 계정에 토큰 크레딧이 충분하며 소진되지 않았는지 확인합니다.
* TVSDK로 보내는 DRM 데이터의 트리플트가 올바른지 확인합니다.ExpressPlay 토큰, 라이센스 서버 URL 및 DRM 유형입니다.
* 두 가지 환경인 테스트 및 제작 환경에서 모든 구성 요소가 사용 중인 ExpressPlay 환경에 대해 동일한 가정을 하고 있는지 확인합니다.
* 서로 다른 브라우저는 일반적으로 DASH 컨텐츠에 대해 하나의 DRM만 지원합니다.
* TVSDK 2.4부터 DASH-LIVE 패키징 프로필만 지원됩니다. (DASH-OnDemand 지원이 로드맵에 있습니다.)
* 디바이스 제조업체의 제한 사항으로 인해 AndroidTV PlayReady 지원이 간헐적으로 제공됩니다. 예를 들자면

   * Razer Forge 장치에 PlayReady 컨텐츠에 문제가 있음
   * Amazon FireTV는 오디오 트랙이 암호화된 DASH 컨텐츠를 사용할 수 없습니다.

* TVSDK 2.4의 경우 AndroidTV 디바이스만 일반적으로 PlayReady 및 Widevine DRM을 지원합니다. 다른 모든 Android 디바이스는 일반적으로 Widevine만 지원합니다.
* TVSDK 2.4부터 현재 Android TVSDK는 PSSH 상자가 .mpd 매니페스트에 있어야 합니다. 이는 DASH 표준과 반대되는 방식이며, PSSH 상자는 내용 자체와 같이 .mpd에서만 모든 위치에 있을 수 있도록 지정합니다.


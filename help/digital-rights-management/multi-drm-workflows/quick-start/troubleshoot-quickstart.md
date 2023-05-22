---
description: 테스트하는 동안 흔히 발생하는 문제에는 ExpressPlay 인증자, 전송 프로토콜 및 필수 서비스 요청 매개 변수가 포함됩니다.
title: 빠른 시작 문제 해결
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 빠른 시작 문제 해결{#troubleshooting-your-quick-start}

테스트하는 동안 흔히 발생하는 문제에는 ExpressPlay 인증자, 전송 프로토콜 및 필수 서비스 요청 매개 변수가 포함됩니다.

다음의 경우 [!DNL curl] 토큰 생성을 위한 ExpressPlay 요청에 실패했습니다. 응답 본문에 실패 이유를 설명하는 오류 메시지가 포함됩니다.

토큰 생성은 성공했지만 콘텐츠가 여전히 재생되지 않는 경우, ExpressPlay 토큰 상환 로그에서 &quot;만료된 토큰&quot;과 같은 오류를 확인하십시오.

토큰 생성이 성공하고 상환에 오류가 없지만 비디오가 여전히 재생되지 않는 경우 CEK가 콘텐츠와 일치하는지, 콘텐츠 형식이 대상 장치의 기능과 일치하는지 확인하십시오.

또한

* 서비스 요청에서 올바른 고객 인증자를 사용하고 있는지 확인하십시오. 테스트 인증자를 사용하려는 경우 실수로 프로덕션 인증자를 사용하기 쉽습니다. 또한 을 사용하고 있는지 확인하십시오 *본인* 인증자. 예를 들어 테스트 중에 다른 사람의 것을 빌릴 수 있습니다. `curl` 명령을 실행하고 인증자에서 해당 인증자로 바꾸는 것을 잊으십시오.

* 요청 또는 매니페스트에서 적절한 전송 프로토콜을 사용 중인지 확인( `https://` 및 `https://`또는 페어플레이의 경우 `skd://` 및 `https://` 및 `https://`.

* 작업 중인 DRM 솔루션에 필요한 모든 쿼리 매개변수를 포함해야 합니다. 예를 들어 PlayReady와 Widevine은 모두 DASH에서 작동하지만 필요한 요청 매개 변수와 패키징 구성이 다르기 때문에 혼동하기 쉽습니다.
* ExpressPlay 계정에 토큰 크레딧이 충분하고 모두 소진되지 않았는지 확인하십시오.
* TVSDK로 전송되는 DRM 데이터의 트리플릿이 올바른지 확인합니다(ExpressPlay 토큰, 라이선스 서버 URL 및 DRM 유형).
* 모든 구성 요소가 테스트 및 프로덕션이라는 두 가지 환경이 있으므로 사용 중인 ExpressPlay 환경과 동일한 가정을 하고 있는지 확인합니다.
* 서로 다른 브라우저는 일반적으로 DASH 콘텐츠에 대해 하나의 DRM만 지원합니다.
* TVSDK 2.4부터는 DASH-LIVE 패키징 프로필만 지원됩니다. (DASH-OnDemand 지원이 로드맵에 있습니다.)
* 장치 제조업체 제한 사항으로 인해 AndroidTV PlayReady 지원이 간헐적으로 중단됩니다. 예를 들자면,

   * razer Forge 장치에 PlayReady 콘텐츠에 문제가 있습니다.
   * Amazon FireTV는 오디오 트랙이 암호화된 DASH 콘텐츠를 사용할 수 없습니다

* TVSDK 2.4부터 AndroidTV 장치만 일반적으로 PlayReady 및 Widevine DRM을 모두 지원합니다. 다른 모든 Android 장치는 일반적으로 Widevine만 지원합니다.
* TVSDK 2.4부터 Android TVSDK를 사용하려면 현재 PSSH 상자가 .mpd 매니페스트에 있어야 합니다. 이는 PSSH 상자가 .mpd뿐만 아니라 콘텐츠 자체에서와 같이 어디에나 있을 수 있음을 지정하는 DASH 표준과 상반됩니다.

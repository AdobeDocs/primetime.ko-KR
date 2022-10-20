---
product: primetime
audience: end-user
user-guide-title: Primetime 참조 구현 도움말
user-guide-description: TVSDK를 이해하고 기능 관리자를 수정하여 개인 플레이어를 사용자 정의할 수 있습니다.
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 7%

---


# Android용 PSDK 1.4 참조 구현 {#reference-implementation}

+ [Android 참조 구현 개요](home.md)
+ Primetime 참조 구현 {#reference}
   + [Primetime 참조 구현을 사용하는 방법](ref-implementation/how-to-use-ref-player.md)
   + [참조 구현 구조](ref-implementation/ref-player-structure.md)
   + 기능 관리자를 사용하는 방법 {#feature-managers}
      + [기능 관리자를 사용하는 방법](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [MediaPlayer에 구성 정보를 전달하여 기능 관리자를 만드는 중..](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [ManagerFactory를 사용하여 기능 설정 또는 해제](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [이벤트 처리](ref-implementation/using-feature-managers/handling-events.md)
   + 개발 환경 설정 {#setup-dev}
      + [개발 환경 설정](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [사전 요구 사항 소프트웨어 다운로드 및 구성](set-up-dev-environment/download-prereqs-android.md)
      + [Primetime 참조 구현 빌드](set-up-dev-environment/install-the-ref-player-project.md)
   + 코드 살펴보기 {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [기능 관리자](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [설정 활동](set-up-dev-environment/exploring-code/settings-activity.md)
      + [카탈로그 형식](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Primetime 광고용 JSON 개체](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [직접 광고 브레이크용 JSON 개체](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [사용자 지정 광고 마커용 JSON 개체](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [권한 리소스 ID에 대한 JSON 개체](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [JSON 피드 형식 예](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + 비디오 재생 구현 {#implement-video}
      + [비디오 재생의 필수 작업](implement-video-playback/video-playback.md)
      + [비디오 재생 활성화](implement-video-playback/enable-video-playback.md)
      + [DRM 콘텐츠 보호](implement-video-playback/content-protection.md)
   + [다중 비트율](implement-video-playback/mbr.md)
   + 광고가 있는 DVR 재생용 플레이어 설정 {#dvr}
      + [광고 삽입 없이 DVR](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [광고 삽입 DVR](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [DVR에 대한 사용자 지정 시작점 선택](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [참조 구현에서 사용자 지정 시작 시간을 설정합니다](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [QoS 재생 및 장치 통계 표시](implement-video-playback/qos-statistics.md)
   + 광고 삽입 {#insert-ads}
      + [광고 삽입](insert-ads/ad-insertion.md)
      + [광고 삽입 유형](insert-ads/ad-insertion-types.md)
      + [광고 추가](insert-ads/add-advertising.md)
      + [관련 API 설명서](insert-ads/aps-callbacks-ad-insertion.md)
   + 오디오 지연 바인딩 {#late-binding-audio}
      + [개요](late-binding-audio/late-binding-audio-overview.md)
      + [지연 바인딩 오디오 통합](late-binding-audio/aa-enable.md)
      + [오디오 트랙 선택](late-binding-audio/select-audio-tracks.md)
      + [관련 API 설명서](late-binding-audio/aa-api-callbacks.md)
   + Primetime 인증 자격 흐름 {#primetime-authentications}
      + [개요](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [자격 관리자 개요](paytvpass-entitlement/entitlement-overvivew.md)
      + [Primetime 인증 통합](paytvpass-entitlement/integrate-pass.md)
      + [Adobe Analytics 보고 구성](paytvpass-entitlement/pass-analytics-setup.md)
      + [관련 API 설명서](paytvpass-entitlement/pass-apis-callbacks.md)
   + Video Analytics {#video-analytics}
      + [Video Analytics](video-analytics/video-analytics-overview.md)
      + [Video Analytics 관리자 만들기](video-analytics/create-video-analytics-manager.md)
      + [Video Analytics 구성](video-analytics/configure-video-analytics-manager.md)
      + [관련 API 설명서](video-analytics/va-apis-callbacks.md)
   + [사용자 지정 사용자 인터페이스 빌드](build-custom-ui.md)
   + [문제 해결](troubleshooting.md)

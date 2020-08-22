---
cloud: experience-cloud
product: primetime
audience: end-user
user-guide-title: Primetime 참조 구현 도움말
user-guide-description: Helps understand the TVSDK and modify the feature managers to customize your personal player.
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Android 참조 구현을 위한 PSDK 1.4 {#reference-implementation}

+ [Android 참조 구현 개요](home.md)
+ Primetime 참조 구현 {#reference}
   + [Primetime 참조 구현 사용 방법](ref-implementation/how-to-use-ref-player.md)
   + [참조 구현 구조](ref-implementation/ref-player-structure.md)
   + 기능 관리자를 사용하는 방법 {#feature-managers}
      + [기능 관리자를 사용하는 방법](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [MediaPlayer에 구성 정보를 전달하여 기능 관리자를 만드는 중..](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [ManagerFactory를 사용하여 기능 활성화 또는 비활성화](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [이벤트 처리](ref-implementation/using-feature-managers/handling-events.md)
   + 개발 환경 설정 {#setup-dev}
      + [개발 환경 설정](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [사전 요구 사항 소프트웨어 다운로드 및 구성](set-up-dev-environment/download-prereqs-android.md)
      + [Primetime 참조 구현 구축](set-up-dev-environment/install-the-ref-player-project.md)
   + 코드 살펴보기 {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [기능 관리자](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [설정 활동](set-up-dev-environment/exploring-code/settings-activity.md)
      + [카탈로그 형식](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Primetime 광고를 위한 JSON 개체](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [직접 광고 나누기를 위한 JSON 개체](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [사용자 정의 광고 마커용 JSON 개체](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [권한 부여 리소스 ID용 JSON 개체](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [JSON 피드 형식 예](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + 비디오 재생 구현 {#implement-video}
      + [비디오 재생에 필수적인 작업](implement-video-playback/video-playback.md)
      + [비디오 재생 활성화](implement-video-playback/enable-video-playback.md)
      + [DRM 컨텐츠 보호](implement-video-playback/content-protection.md)
   + [다양한 비트 전송률](implement-video-playback/mbr.md)
   + 광고가 포함된 DVR 재생을 위한 플레이어 설정 {#dvr}
      + [광고 삽입 없이 DVR](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [광고 삽입 시 DVR](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [DVR에 대한 사용자 정의 시작 지점 선택](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [참조 구현에서 사용자 지정 시작 시간 설정](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [QoS 재생 및 디바이스 통계 표시](implement-video-playback/qos-statistics.md)
   + 광고 삽입 {#insert-ads}
      + [광고 삽입](insert-ads/ad-insertion.md)
      + [광고 삽입 유형](insert-ads/ad-insertion-types.md)
      + [광고 추가](insert-ads/add-advertising.md)
      + [관련 API 설명서](insert-ads/aps-callbacks-ad-insertion.md)
   + 지연 바인딩 오디오 {#late-binding-audio}
      + [개요](late-binding-audio/late-binding-audio-overview.md)
      + [지연 바인딩 오디오 통합](late-binding-audio/aa-enable.md)
      + [오디오 트랙 선택](late-binding-audio/select-audio-tracks.md)
      + [관련 API 설명서](late-binding-audio/aa-api-callbacks.md)
   + Primetime 인증 권한 부여 흐름 {#primetime-authentications}
      + [개요](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [권한 부여 관리자 개요](paytvpass-entitlement/entitlement-overvivew.md)
      + [Primetime 인증 통합](paytvpass-entitlement/integrate-pass.md)
      + [Adobe Analytics 보고 구성](paytvpass-entitlement/pass-analytics-setup.md)
      + [관련 API 설명서](paytvpass-entitlement/pass-apis-callbacks.md)
   + 비디오 분석 {#video-analytics}
      + [비디오 분석](video-analytics/video-analytics-overview.md)
      + [비디오 분석 관리자 만들기](video-analytics/create-video-analytics-manager.md)
      + [비디오 분석 구성](video-analytics/configure-video-analytics-manager.md)
      + [관련 API 설명서](video-analytics/va-apis-callbacks.md)
   + [사용자 정의 유저 인터페이스 구축](build-custom-ui.md)
   + [문제 해결](troubleshooting.md)

---
description: iOS용 TVSDK에는 다양한 기능이 포함되어 있습니다.
title: Primetime TVSDK 기능
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Primetime TVSDK 기능 {#primetime-tvsdk-features}

iOS용 TVSDK에는 다양한 기능이 포함되어 있으며 다음과 같은 주요 기능을 제공합니다.

* VOD 및 라이브/선형 재생

   * 재생 헤드 위치를 재생, 중지, 일시 중지, 탐색 및 검색하는 메서드를 포함한 재생 창 관리
   * 전체 이벤트 재생 지원
   * 자막 (608, WebVTT) 및 접근성 향상을 위한 대체 형태의 오디오
   * DVR 기능
   * ABR(적응형 비트 전송률) 논리 및 ABR 컨트롤 초기 설정
   * 비HLS 및 HLS 태그 구독
   * 라이브 매니페스트 장애 조치(failover) 지원

* 광고

   * VPAID 2.0
   * 클라이언트측 광고 결합

      * VAST/VMAP 지원을 포함한 원활한 광고 삽입
      * 광고에 대한 사용자 지정 큐 태그 지원
      * C3 광고 표시, 교체 및 삭제 지원
      * 사용자 정의 가능한 컨텐츠/광고 삽입 워크플로(일시 중단 신호 포함)

* 콘텐츠 보호

   * DRM(디지털 권한 관리) 관련 서비스 액세스
   * 암호화되지 않았거나 보호된 HTTP 라이브 스트리밍(PHLS)을 사용한 HLS 스트림 재생
   * DRM 정책 기반 해상도 기반 출력 제어

* 비디오 및 광고 추적

   * QoS 이벤트 추적
   * TVSDK 및 애플리케이션이 비디오, 광고 및 기타 요소의 상태와 로그 활동에 대해 비동기적으로 통신할 수 있도록 도와주는 알림입니다
   * Adobe Analytics 및 하트비트 지원과의 통합

* 로깅

   * 디버그 로깅

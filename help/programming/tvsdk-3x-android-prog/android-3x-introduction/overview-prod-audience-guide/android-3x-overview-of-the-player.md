---
description: Android 3.4용 TVSDK에는 플레이어에서 구현할 수 있는 다양한 기능이 포함되어 있습니다.
seo-description: Android 3.4용 TVSDK에는 플레이어에서 구현할 수 있는 다양한 기능이 포함되어 있습니다.
seo-title: Primetime TVSDK 기능
title: Primetime TVSDK 기능
uuid: 6e26c09c-2858-47d1-80e8-1d7c6a468b86
translation-type: tm+mt
source-git-commit: ad58732842eb651514a47dd565e31e3d98a84c46
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Primetime TVSDK 기능 {#primetime-tvsdk-features}

Android 3.9용 TVSDK에는 플레이어에서 구현할 수 있는 다양한 기능이 포함되어 있습니다.

TVSDK 기능:

* **VOD 및 실시간/선형 재생**

   * 재생, 중지, 일시 중지, 검색 및 재생 헤드 위치를 가져오는 방법을 비롯하여 재생 창 관리
   * 전체 이벤트 재생 지원
   * 액세스 가능성 향상을 위한 자막(608, 708, WebVTT) 및 오디오 대체 형식
   * 캡션의 텍스트 스타일 제어
   * DVR 기능, 빨리 감기 및 빨리 되감기(후자를 *트릭-플레이 모드*&#x200B;라고 함)
   * ABR(응용 비트 전송률) 로직 및 ABR 컨트롤의 초기 설정
   * 실시간 매니페스트 장애 조치 지원
   * 조정 가능한 재생 버퍼
   * 조각 기간, 크기 및 다운로드 시간 추적 지원

* **광고**

   * VPAID 2.0
   * 클라이언트측 광고 연결

      * VAST/VMAP 지원을 비롯한 완벽한 광고 삽입
      * 광고에 대한 사용자 정의 큐 태그 지원
      * C3 광고 표시, 교체 및 삭제 지원
      * 일시 중단 신호를 비롯한 사용자 정의 가능한 컨텐츠/광고 삽입 워크플로우

* **컨텐츠 보호**

   * 디지털 저작권 관리(DRM) 관련 서비스 이용
   * 암호화되지 않은 HLS 스트림 또는 보호된 PHLS(HTTP Live Streaming)를 통한 HLS 재생
   * DRM 정책을 기반으로 하는 해상도 기반의 출력 제어

* **비디오 및 광고 추적**

   * QoS 이벤트 추적
   * TV SDK 및 응용 프로그램이 비디오, 광고 및 기타 요소의 상태를 비동기식으로 알리는 데 도움이 되는 알림입니다. 알림도 활동을 기록합니다.

* **로깅**

   * 디버그 로깅
   * 조각 기간, 크기 및 다운로드 시간에 대한 추적 지원.

* **안전한 전달**

   * TVSDK에서 시작된 모든 호출에 대한 HTTPS(Secure Delivery) 지원
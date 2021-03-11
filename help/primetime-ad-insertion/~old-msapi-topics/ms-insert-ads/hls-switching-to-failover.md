---
description: Apple HLS 스택은 기본 세트의 스트림을 검색할 수 없는 경우 페일오버/백업 스트림으로 전환하는 것을 지원합니다. Apple HLS 장치의 경우 장애 조치를 용이하게 하기 위해 매니페스트 서버에 신호를 보내 마스터 재생 목록에서 식별된 기본 및 장애 조치 스트림을 자체 UUID로 분리되어 있는 세트로 처리할 수 있습니다.
title: 페일오버/백업 스트림으로 HLS 플레이어 전환 촉진
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 페일오버/백업 스트림으로 HLS 플레이어 전환 촉진 {#facilitating-hls-player-switching-to-failover-backup-streams}

Apple HLS 스택은 기본 세트의 스트림을 검색할 수 없는 경우 페일오버/백업 스트림으로 전환하는 것을 지원합니다. Apple HLS 장치의 경우 장애 조치를 용이하게 하기 위해 매니페스트 서버에 신호를 보내 마스터 재생 목록에서 식별된 기본 및 장애 조치 스트림을 자체 UUID로 분리되어 있는 세트로 처리할 수 있습니다.

Apple HLS 장치에서 페일오버 또는 백업 스트림으로 쉽게 전환하기 위해 Bootstrap URL에 `ptfailover` 매개 변수를 지정할 수 있습니다. 이 매개 변수를 제공하면 매니페스트 서버가 각 장애 조치(failover) 세트에 대해 별도의 재생 세션(연결된 광고를 결정)을 만듭니다.

## 세부 정보

Bootstrap 요청에 `ptfailover=true`을(를) 포함할 때 SSAI가 페일오버/백업으로 HLS 전환을 처리하는 방법:

* 마스터 재생 목록에 기본 및 백업 세트가 포함된 경우:

   * 매니페스트 서버는 `BANDWIDTH` 속성 및 AV 스트림 URL의 구문 분석 순서를 사용하여 다른 장애 조치(failover) 세트에 대한 AV 스트림 URL을 식별합니다. 별도의 UUID로 식별되는 별도의 내부 재생 세션을 만들고 다른 재생 세션을 식별하는 다른 UUID가 있는 매니페스트 서버를 가리키는 스트림 URL을 만듭니다.
   * 매니페스트 서버는 일치하는 `RESOLUTION` 속성과 I-Frame 스트림 URL의 구문 분석 순서를 사용하여 다른 장애 조치(failover) 세트에 대한 I-Frame 스트림 URL을 식별합니다. SSAI는 I-Frame 스트림 URL에 대한 연관된 AV 스트림을 식별하는 UUID를 사용합니다.
   * 이 기능의 경우 매니페스트 서버는 마스터 재생 목록에서 URI 특성이 없는 `EXT-X-MEDIA` 그룹만 지원합니다.
   * 매니페스트 서버는 `X-Object-Too-Old: true` 헤더가 있는 CDN의 404 오류 응답을 감지하고 해당 응답을 플레이어로 보낼 때 상태 코드와 헤더를 유지합니다.

* 프리롤 광고는 기본 세트에만 추가됩니다.장애 조치(failover) 세트에서 완전히 비활성화되어 플레이어가 장애 조치(failover) 스트림으로 전환될 때 오류 및/또는 중복된 프리롤 광고를 방지합니다.


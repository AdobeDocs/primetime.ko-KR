---
description: Apple HLS 스택은 기본 세트의 스트림을 검색할 수 없는 경우 페일오버/백업 스트림으로 전환을 지원합니다. Apple HLS 장치의 경우 장애 조치를 용이하게 하기 위해 매니페스트 서버에 신호를 보내 마스터 재생 목록에 식별된 기본 및 장애 조치 스트림을 분리된 세트(자체 UUID 포함)로 처리할 수 있습니다.
title: HLS 플레이어에서 장애 조치/백업 스트림으로 전환 촉진
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# HLS 플레이어에서 장애 조치/백업 스트림으로 전환 촉진 {#facilitating-hls-player-switching-to-failover-backup-streams}

Apple HLS 스택은 기본 세트의 스트림을 검색할 수 없는 경우 페일오버/백업 스트림으로 전환을 지원합니다. Apple HLS 장치의 경우 장애 조치를 용이하게 하기 위해 매니페스트 서버에 신호를 보내 마스터 재생 목록에 식별된 기본 및 장애 조치 스트림을 분리된 세트(자체 UUID 포함)로 처리할 수 있습니다.

Apple HLS 장치에서 페일오버 또는 백업 스트림으로 쉽게 전환하려면 다음을 지정할 수 있습니다. `ptfailover` Bootstrap URL의 매개 변수. 이 매개 변수를 제공하면 매니페스트 서버는 각 장애 조치(failover) 세트에 대해 별도의 재생 세션(결합된 광고를 결정함)을 만듭니다.

## 세부 사항

다음을 포함할 때 SSAI가 페일오버/백업으로 전환하는 HLS를 처리하는 방법 `ptfailover=true` Bootstrap 요청에서:

* 마스터 재생 목록에 기본 및 백업 세트가 포함된 경우:

   * 매니페스트 서버는 다음을 사용하여 서로 다른 장애 조치(failover) 집합에 대한 AV 스트림 URL을 식별합니다 `BANDWIDTH` 속성 및 AV 스트림 URL의 구문 분석 순서. 별도의 내부 재생 세션(별도의 UUID로 식별됨)을 만들고 매니페스트 서버를 가리키는 스트림 URL을 만들며 다른 재생 세션을 식별하는 다른 UUID가 있습니다.
   * 매니페스트 서버는 일치하는 항목을 사용하여 서로 다른 장애 조치(failover) 집합에 대한 I-Frame 스트림 URL을 식별합니다 `RESOLUTION` 속성 및 I-Frame 스트림 URL의 구문 분석 순서입니다. SSAI는 SSAI를 가리키는 I-Frame 스트림 URL에 대해 연관된 AV 스트림을 식별하는 UUID를 사용합니다.
   * 이 기능의 경우 매니페스트 서버는 `EXT-X-MEDIA` 마스터 재생 목록에 URI 특성이 없는 그룹입니다.
   * 매니페스트 서버는 CDN에서 404 오류 응답을 `X-Object-Too-Old: true` 를 클릭하고, 플레이어에 해당 응답을 보낼 때 상태 코드와 헤더를 유지합니다.

* 프리롤 광고는 기본 세트에만 추가됩니다. 플레이어가 페일오버 스트림으로 전환할 때 잘못되거나 중복되는 프리롤 광고를 방지하기 위해 페일오버 세트에서 완전히 비활성화됩니다.


---
description: PABI(Partial Ad Break Insertion) 기능은 사용자가 미드롤 브레이크 내에서 라이브 스트림에 연결할 경우 프리롤 광고 또는 슬레이트 대신 미드롤 광고가 표시되는 TV 유사 경험을 모방합니다.
title: 부분 광고 브레이크 삽입
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 부분 광고 브레이크 삽입 {#partial-ad-break-insertion}

PABI(Partial Ad Break Insertion) 기능은 사용자가 미드롤 브레이크 내에서 라이브 스트림에 연결할 경우 프리롤 광고 또는 슬레이트 대신 미드롤 광고가 표시되는 TV 유사 경험을 모방합니다.

광고 서버에서 라이브 스트림에 대한 프리롤 광고를 반환하면, 매니페스트 서버는 라이브 포인트 앞에 프리롤 광고 브레이크를 삽입하고, TIMEOFFSET 값이 프리롤 광고 브레이크의 시작을 가리키는 EXT-X-START 태그를 삽입합니다. 이 기본 비헤이비어는 라이브 포인트에서 콘텐츠가 재생되기 전에 전체 프리롤 광고 브레이크를 재생하도록 합니다. 라이브 포인트가 미드롤 광고 브레이크 근처에 있을 때 사용자가 스트림에 참여하는 경우 라이브 포인트에서 미드롤 광고 브레이크 앞에 프리롤 광고 브레이크가 표시됩니다.

PABI 기능은 매니페스트 서버가 프리롤 광고 브레이크를 무시하고 EXT-X-START:TIMEOFFSET 값을 라이브 포인트에 있는 미드롤 광고의 시작으로 설정하도록 지시합니다. 이렇게 하면 사용자가 프리롤 광고 브레이크를 볼 필요 없이 라이브 포인트에서 현재 재생 중인 전체 미드롤 광고를 볼 수 있습니다.

>[!NOTE]
>
>이 기능은 라이브 스트림에만 사용할 수 있습니다. 매니페스트 서버는 기본적으로 VOD 재생 목록 맨 위에 프리롤 광고 브레이크를 삽입합니다.

>[!NOTE]
>
>PABI를 활성화하려면 다음을 지정해야 합니다 [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) 부트스트랩 URL

>[!NOTE]
>
>다음 [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) 는 재생 목록 내에서 선호하는 시작 지점을 나타내는 표준 HLS 태그입니다.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* 클라이언트가 추적 비콘 실행을 보다 세밀하게 제어할 수 있으므로 클라이언트측 추적을 사용합니다.
* 플레이어가 EXT-X-START를 지원하는 경우 부분 광고 브레이크는 서버측 추적 모드에서만 사용해야 합니다.
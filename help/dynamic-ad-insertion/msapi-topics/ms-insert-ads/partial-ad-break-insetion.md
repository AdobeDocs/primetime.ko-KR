---
description: PABI(Partial Ad Break Insertion) 기능은 TV와 유사한 TV 경험을 모방하여 사용자가 미드롤 브레이크에서 라이브 스트림에 참여하는 경우 프리롤 광고 또는 슬레이트가 아닌 미드롤 광고를 표시합니다.
seo-description: PABI(Partial Ad Break Insertion) 기능은 TV와 유사한 TV 경험을 모방하여 사용자가 미드롤 브레이크에서 라이브 스트림에 참여하는 경우 프리롤 광고 또는 슬레이트가 아닌 미드롤 광고를 표시합니다.
seo-title: 부분 광고 나누기 삽입
title: 부분 광고 나누기 삽입
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 부분 광고 나누기 삽입 {#partial-ad-break-insertion}

PABI(Partial Ad Break Insertion) 기능은 TV와 유사한 TV 경험을 모방하여 사용자가 미드롤 브레이크에서 라이브 스트림에 참여하는 경우 프리롤 광고 또는 슬레이트가 아닌 미드롤 광고를 표시합니다.

광고 서버가 라이브 스트림에 대한 프리롤 광고를 반환하면 매니페스트 서버가 라이브 포인트 앞에 프리롤 광고 브레이크를 삽입하고 프리롤 광고 브레이크의 시작을 가리키는 TIMEOFFSET 값과 함께 EXT-X-START 태그를 삽입합니다. 이러한 기본 동작을 통해 전체 프리롤 광고 브레이크가 라이브 포인트에서 컨텐츠 전에 재생되도록 할 수 있습니다. 사용자가 라이브 포인트가 중간 롤 광고 브레이크 근처에 있을 때 스트림에 참여하는 경우, 라이브 포인트에서 미드롤 광고 중단 전에 프리롤 광고 브레이크가 표시됩니다.

PABI 기능은 매니페스트 서버에서 프리롤 광고 브레이크를 무시하고 EXT-X-START:TIMEOFFSET 값을 라이브 포인트에 있는 중간 롤 광고의 시작으로 설정합니다. 그러면 사용자는 프리롤 광고 브레이크 없이 현재 라이브 지점에서 재생되는 전체 미드롤 광고를 볼 수 있습니다.

>[!NOTE]
>
>이 기능은 실시간 스트림에서만 사용할 수 있습니다. 매니페스트 서버는 기본적으로 VOD 재생 목록에 프리롤 광고 브레이크를 삽입합니다.

>[!NOTE]
>
>PABI를 활성화하려면 부트스트랩 URL에서 [query_params](../../msapi-topics/ms-getting-started/ms-api-query-params.md) 를 지정해야 합니다.

>[!NOTE]
>
>EXT [-X-START는](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) 표준 HLS 태그로 재생 목록에서 원하는 시작점을 나타냅니다.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* 클라이언트가 추적 비콘 실행을 보다 강력하게 제어하기 때문에 클라이언트측 추적을 사용합니다.
* 플레이어가 EXT-X-START를 지원하는 경우 부분 광고 나누기는 서버측 추적 모드에서만 사용해야 합니다.
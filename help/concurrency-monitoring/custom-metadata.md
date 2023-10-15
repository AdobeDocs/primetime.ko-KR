---
title: 사용자 지정 메타데이터
description: 사용자 지정 메타데이터
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---



# 사용자 지정 메타데이터 {#cm}

>[!NOTE]
>
> 이 페이지는 새 통합에 대해 더 이상 권장되지 않는 이전 버전의 API에 적용되므로 더 이상 사용되지 않습니다

이 서비스를 통해 클라이언트는 쿼리 및 의사 결정 모두에서 표준 및 사용자 정의 필드를 모두 사용할 수 있습니다. 표준 필드는 스트림 생성에 필요하거나 서버에서 생성되므로 모든 스트림에 대해 항상 사용할 수 있습니다.

* 애플리케이션
* mvpd
* accountId
* streamId
* streamStart
* 개시자


사용자 지정 필드는 양식 또는 쿼리 문자열 매개 변수로 스트림 초기화 시 전달되는 모든 키/값 쌍입니다. 그런 다음 표준 및 사용자 정의 필드를 모두 다음 시나리오에서 사용할 수 있습니다(자세한 내용은 관련 API 리소스에 대한 실제 설명서 아래 참조).

* 계정(/streams 리소스)에 대한 스트림 목록을 가져올 때 필드 쿼리 문자열 매개 변수를 통해 추가 필드 요청
* 그룹화할 차원(/activity 리소스)을 지정하여 계정 활동 분류
* 필드 값 또는 카디널리티를 기반으로 서버측 정책 정의(예: 명확성을 위해 의사 SQL 사용):
* 특정 필드 값에만 적용되도록 정책을 구성합니다(예: 전용 iOS 정책: WHERE osType IS &#39;iOS&#39;).
* 주어진 필드에 대한 고유 값의 수를 제한합니다(예: X개 이하의 고유 장치: HAVING DISTINCT COUNT(deviceId) >= 2)
* 필드 값당 활성 스트림 수 제한(예: 단일 장치 유형에 대해 최대 X개의 활성 스트림 제한: COUNT(streamId)가 있는 GROUP BY deviceType >= 3)


전송되는 이러한 키/값에 따라 다른 규칙을 설정할 수 있습니다. 이는 다음 라인에 해당할 수 있습니다.

1. 고객은 매개 변수 그룹을 보내려고 하며, 이 매개 변수 그룹에는 &quot;SPORTS&quot; 및 &quot;KIDS&quot; 값이 있습니다.
1. 그런 다음 앱에서 다음을 수행해야 합니다.
   * 스포츠 채널의 경우 스트림 초기화에서 앱이 전송하는 것입니다 ***type=SPORTS*** 쿼리 매개 변수로
   * 어린이 관련 콘텐츠가 있는 채널의 경우, 스트림 초기화에서 앱이 전송하는 것입니다 ***type=KIDS*** 쿼리 매개 변수로
1. 그런 다음 다음과 같은 정책을 정의할 수 있습니다.
   * `GROUP by type HAVING COUNT(streamID) < 4) IF type=KIDS`
   * `GROUP by type HAVING COUNT(streamID) < 2) IF type=SPORTS`
1. 이는 기본적으로 사용자가 스포츠를 시청할 때는 1개 이상의 디바이스에서 스포츠를 시청할 수 없지만, 사용자가 키즈 컨텐츠를 시청할 때는 최대 3개의 디바이스에서 볼 수 있음을 의미합니다.

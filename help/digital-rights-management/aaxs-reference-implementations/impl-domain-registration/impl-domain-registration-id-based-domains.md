---
title: ID 기반 도메인
description: ID 기반 도메인
copied-description: true
exl-id: de7b6c8a-5227-4679-933a-3278921903d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# ID 기반 도메인 {#identity-based-domains}

이 사용 사례에서는 인증된 각 사용자가 자체 도메인을 가지며 특정 개수의 장치가 도메인에 가입할 수 있습니다. 참조 구현과 함께 이 유형의 도메인을 사용하려면 도메인 등록이 필요함을 지정하는 정책을 만들어야 합니다. 도메인 서버 URL에 대해 서버의 호스트 및 포트를 지정하고 사용자 이름/암호 인증이 필요함을 지정합니다.

참조 구현은 도메인 등록을 위해 다음 논리를 구현합니다.

1. 이 사용자에게 할당할 도메인 이름을 결정합니다. 도메인 이름은 * 입니다. `namequalifier:username`* 인증 토큰에서 추출됩니다. 인증 토큰이 없으면 오류 DOM_AUTHENTICATION_REQUIRED(503)를 반환합니다.
1. 에서 도메인 이름 조회 `DomainServerInfo` 테이블. 항목을 찾을 수 없으면 테이블에 항목을 삽입합니다(기본값은 인증 필요, 최대 도메인 멤버십=5).
1. 장치가 도메인에 이미 등록되어 있는지 확인합니다.

   1. 에서 도메인 이름 조회 `UserDomainMembership` 테이블. 발견된 각 컴퓨터 ID에 대해 요청의 컴퓨터 ID와 비교합니다. 새 컴퓨터인 경우 항목을 `UserDomainMembership` 테이블. 그런 다음 일치하는 레코드를 찾습니다. `UserDomainRefCount` 테이블. 이 컴퓨터 GUID에 대한 항목이 없으면 레코드를 추가합니다.

   1. 새 디바이스이고 최대 멤버십에 이미 도달한 경우 오류 DOM_LIMIT_REACHED(502)를 반환합니다.

1. DomainKeys 테이블에서 이 도메인의 모든 도메인 키를 조회합니다.

   1. If `DomainServerInfo` 는 키를 롤오버하고 새 키 쌍을 생성하여 `DomainKeys` 테이블(키 버전이 가장 높은 기존 키보다 높은 경우) 및 의 &quot;키 롤오버 필수&quot; 플래그 재설정 `DomainServerInfo`.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

참조 구현인 에서는 도메인 등록 취소를 위해 다음 논리를 구현합니다.

1. 이 사용자에게 할당할 도메인 이름을 결정합니다. 도메인 이름은 다음과 같습니다 *namequalifier:username* 인증 토큰에서 추출되었습니다. 인증 토큰이 없으면 오류 DOM_AUTHENTICATION_REQUIRED(503)를 반환합니다.
1. 에서 요청된 도메인 이름을 조회합니다. `DomainServerInfo` 테이블.
1. 에서 도메인 이름 조회 `UserDomainMembership` 테이블. 발견된 각 컴퓨터 ID에 대해 요청의 컴퓨터 ID와 비교합니다. 에서 해당 항목 찾기 `UserDomainRefCount` 테이블. 일치하는 항목을 찾을 수 없으면 DEREG_DENIED 오류를 반환합니다(401).

1. 미리 보기 요청이 아닌 경우에서 항목을 삭제합니다. `UserDomainRefCount` 테이블. 시스템에 대한 해당 테이블에 더 이상 항목이 없는 경우에서 항목을 삭제합니다. `UserDomainMembership` 및 의 &quot;키 롤오버 필수&quot; 플래그 설정 `DomainServerInfo`.

이 사용 사례에서는 각 사용자가 적은 수의 시스템을 등록할 수 있으므로 전체 시스템 ID와 를 사용할 수 있습니다. `matches()` 시스템을 정확하게 카운트하는 방법. 그러나 사용자는 이 컴퓨터에서 여러 AIR 애플리케이션이나 다른 브라우저의 플레이어를 통해 여러 번 등록할 수 있으므로 서버는 등록 취소가 정확하게 계산되도록 참조 카운트를 유지해야 합니다. 컴퓨터의 모든 도메인 토큰이 렌더링될 때까지 등록 취소를 완료된 것으로 간주할 수 없습니다.

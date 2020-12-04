---
seo-title: ID 기반 도메인
title: ID 기반 도메인
uuid: 34cad19b-1adb-4e0c-ac59-50632f6988f7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# ID 기반 도메인 {#identity-based-domains}

이 경우 인증된 각 사용자마다 자체 도메인이 있으며 특정 수의 장치가 도메인에 참여할 수 있습니다. 참조 구현과 함께 이 유형의 도메인을 사용하려면 도메인 등록이 필요한 정책을 만듭니다. 도메인 서버 URL에 대한 서버의 호스트 및 포트를 지정하고 사용자 이름/암호 인증이 필요합니다.

참조 구현에서는 도메인 등록에 대한 다음 논리를 구현합니다.

1. 이 사용자에게 할당할 도메인 이름을 결정합니다. 도메인 이름은 인증 토큰에서 * `namequalifier:username`*이 추출됩니다. 인증 토큰이 없는 경우 오류 DOM_AUTHENTICATION_REQUIRED(503)를 반환합니다.
1. `DomainServerInfo` 테이블에서 도메인 이름을 조회합니다. 항목을 찾을 수 없으면 표에 항목을 삽입합니다. 기본값은 인증이 필요하며 최대 도메인 구성원 자격=5).
1. 장치가 도메인에 이미 등록되어 있는지 확인합니다.

   1. `UserDomainMembership` 테이블에서 도메인 이름을 조회합니다. 검색된 각 컴퓨터 ID에 대해 요청의 컴퓨터 ID와 비교합니다. 새 컴퓨터인 경우 `UserDomainMembership` 테이블에 항목을 추가합니다. 그런 다음 `UserDomainRefCount` 테이블에서 일치하는 레코드를 찾습니다. 이 컴퓨터 GUID에 대한 항목이 없으면 레코드를 추가하십시오.

   1. 새 장치이고 최대 멤버십에 이미 도달한 경우 오류 DOM_LIMIT_REACHED(502)를 반환합니다.

1. DomainKeys 테이블에서 이 도메인에 대한 모든 도메인 키를 조회합니다.

   1. `DomainServerInfo`이 키를 롤오버해야 함을 나타내는 경우, 새 키 쌍을 생성하고, `DomainKeys` 테이블에 저장하고(키 버전이 가장 높은 기존 키보다 높음), `DomainServerInfo`에서 &quot;키 롤오버 필요&quot; 플래그를 재설정합니다.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

참조 구현에서는 도메인 등록 취소에 대한 다음 논리를 구현합니다.

1. 이 사용자에게 할당할 도메인 이름을 결정합니다. 도메인 이름은 인증 토큰에서 추출한 *namequalifier:username*&#x200B;입니다. 인증 토큰이 없는 경우 오류 DOM_AUTHENTICATION_REQUIRED(503)를 반환합니다.
1. `DomainServerInfo` 테이블에서 요청된 도메인 이름을 조회합니다.
1. `UserDomainMembership` 테이블에서 도메인 이름을 조회합니다. 검색된 각 컴퓨터 ID에 대해 요청의 컴퓨터 ID와 비교합니다. `UserDomainRefCount` 테이블에서 해당 항목을 찾습니다. 일치하는 항목을 찾을 수 없으면 오류 DEREG_DENIED(401)를 반환합니다.

1. 미리 보기 요청이 아닌 경우 `UserDomainRefCount` 테이블에서 항목을 삭제합니다. 컴퓨터에 대한 해당 테이블에 항목이 더 이상 없으면 `UserDomainMembership`에서 항목을 삭제하고 `DomainServerInfo`에서 &quot;키 롤오버 필수&quot; 플래그를 설정합니다.

이 경우 각 사용자는 적은 수의 컴퓨터를 등록할 수 있으므로 전체 컴퓨터 ID와 `matches()` 메서드를 사용하여 컴퓨터를 정확하게 계산할 수 있습니다. 그러나 사용자가 이 시스템에서 여러 번 등록할 수 있으므로(여러 AIR 애플리케이션 또는 다른 브라우저의 플레이어를 통해) 서버에서 참조 카운트를 유지해야 하므로 등록 취소 횟수가 정확하게 카운트될 수 있습니다. 컴퓨터의 모든 도메인 토큰이 투항될 때까지 등록 해제를 완료로 간주할 수 없습니다.

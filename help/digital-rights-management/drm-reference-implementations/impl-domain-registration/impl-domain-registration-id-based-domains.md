---
title: ID 기반 도메인 등록 논리
description: ID 기반 도메인 등록 논리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# ID 기반 도메인 등록 논리{#identity-based-domain-registration-logic}

## 도메인 등록 논리 {#section_149C247458954877AF158B4A09A8526B}

참조 구현은 ID 기반 도메인 등록에 대해 다음 논리를 적용합니다.

1. 지정된 사용자에게 할당할 도메인 이름을 결정합니다.

   도메인 이름( `namequalifier:username`)가 인증 토큰에서 추출됩니다. 토큰을 사용할 수 없으면 오류가 발생합니다.
1. 에서 도메인 이름 조회 `DomainServerInfo` 테이블.

   항목이 없으면 항목을 삽입합니다. 기본값은 다음과 같습니다.

   * `authentication required`
   * `max domain membership=5`

   .

1. 장치가 도메인에 등록되었는지 확인하려면:

   1. 조회 `domainname` 다음에서 `UserDomainMembership` 표:

      1. 있는 각 컴퓨터 ID에 대해 요청에서 해당 ID를 컴퓨터 ID와 비교합니다.
      1. 새 컴퓨터인 경우 항목을 `UserDomainMembership` 테이블.
      1. 에서 일치하는 레코드 검색 `UserDomainRefCount` 테이블.
      1. 이 컴퓨터 GUID에 대한 항목이 없으면 레코드를 추가합니다.

   1. 새 디바이스인 경우 및 `Max Membership` 값에 도달했습니다. 오류 를 반환합니다.

1. 에서 이 도메인의 모든 도메인 키 조회 `DomainKeys` 표:

   1. If `DomainServerInfo` 키를 롤오버하고 새 키 쌍을 생성해야 함을 나타냅니다.
   1. 에 쌍을 저장합니다. `DomainKeys` 테이블, 가장 높은 기존 키보다 한 단계 높은 키 버전 포함
   1. 재설정 `Key Rollover Required` 플래그 `DomainServerInfo`.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

## 도메인 등록 취소 논리 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

참조 구현은 ID 기반 도메인 등록 취소에 대해 다음 논리를 적용합니다.

1. 이 사용자에게 할당할 도메인 이름을 결정합니다.

   도메인 이름은 다음과 같습니다. `namequalifier:username`: 인증 토큰에서 추출됩니다. 사용 가능한 토큰이 없으면 오류를 반환합니다. `DOM_AUTHENTICATION_REQUIRED (503)` 발생합니다.
1. 에서 요청된 도메인 이름을 조회합니다. `DomainServerInfo` 테이블.
1. 에서 도메인 이름 조회 `UserDomainMembership` 테이블.
1. 찾은 각 컴퓨터 ID를 요청에서 컴퓨터 ID와 비교합니다.
1. 에서 해당 항목을 찾습니다. `UserDomainRefCount` 테이블.

   일치하는 항목이 없으면 오류 를 반환합니다.

1. 미리보기 요청이 아닌 경우 `UserDomainRefCount` 테이블.
1. 시스템에 대한 해당 테이블에 추가 항목이 없는 경우에서 항목을 삭제합니다. `UserDomainMembership` 및 설정 [!DNL Key Rollover Required] 의 플래그 `DomainServerInfo` 속성.

각 사용자는 소수의 시스템을 등록할 수 있으므로 전체 시스템 ID와 `matches()` 메서드를 사용하여 컴퓨터를 계산합니다. 사용자는 여러 브라우저에서 여러 AIR 애플리케이션 또는 플레이어를 통해 여러 번 등록할 수 있으므로, 서버는 등록 취소도 카운트될 수 있도록 참조 카운트를 유지 관리해야 합니다.

>[!NOTE]
>
>컴퓨터의 모든 도메인 토큰이 렌더링될 때까지 등록 취소가 완료되지 않습니다.

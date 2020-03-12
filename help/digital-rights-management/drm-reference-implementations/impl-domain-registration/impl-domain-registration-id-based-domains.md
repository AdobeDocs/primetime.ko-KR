---
description: 'null'
seo-description: 'null'
seo-title: ID 기반 도메인 등록 논리
title: ID 기반 도메인 등록 논리
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# ID 기반 도메인 등록 논리{#identity-based-domain-registration-logic}

## 도메인 등록 논리 {#section_149C247458954877AF158B4A09A8526B}

참조 구현은 ID 기반 도메인 등록에 대해 다음 논리를 적용합니다.

1. 지정된 사용자에게 할당할 도메인 이름을 결정합니다.

   도메인 이름( `namequalifier:username`)이 인증 토큰에서 추출됩니다. 토큰을 사용할 수 없는 경우 오류가 발생합니다.
1. 테이블에서 도메인 이름을 `DomainServerInfo` 찾습니다.

   항목을 찾을 수 없으면 항목을 삽입합니다. 기본값은 다음과 같습니다.

   * `authentication required`
   * `max domain membership=5`
   .

1. 장치가 도메인에 등록되어 있는지 확인하려면:

   1. 아래 표에서 `domainname` 위의 `UserDomainMembership` 표를 찾아보십시오.

      1. 있는 각 컴퓨터 ID에 대해 ID와 요청의 컴퓨터 ID를 비교합니다.
      1. 새 컴퓨터인 경우 `UserDomainMembership` 표에 항목을 추가합니다.
      1. 테이블에서 일치하는 레코드를 `UserDomainRefCount` 검색합니다.
      1. 이 컴퓨터 GUID에 대한 항목이 없으면 레코드를 추가하십시오.
   1. 새 장치이고 `Max Membership` 값에 도달한 경우 오류를 반환합니다.


1. 다음 `DomainKeys` 표에서 이 도메인에 대한 모든 도메인 키를 찾습니다.

   1. 키를 롤오버해야 `DomainServerInfo` 한다고 표시되면 새 키 쌍을 생성합니다.
   1. 표에서 가장 높은 기존 키보다 높은 키 버전을 사용하여 쌍을 `DomainKeys` 저장합니다.
   1. 에서 `Key Rollover Required` 플래그를 재설정합니다 `DomainServerInfo`.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

## 도메인 등록 취소 로직 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

참조 구현은 ID 기반 도메인 등록 취소에 대해 다음 논리를 적용합니다.

1. 이 사용자에게 할당할 도메인 이름을 결정합니다.

   도메인 이름은 `namequalifier:username`인증 토큰에서 추출됩니다. 사용할 수 있는 토큰이 없으면 반환 오류가 `DOM_AUTHENTICATION_REQUIRED (503)` 발생합니다.
1. 테이블에서 요청된 도메인 이름을 `DomainServerInfo` 찾습니다.
1. 테이블에서 도메인 이름을 `UserDomainMembership` 찾습니다.
1. 찾은 각 컴퓨터 ID를 요청의 컴퓨터 ID와 비교합니다.
1. 테이블에서 해당 항목을 `UserDomainRefCount` 찾습니다.

   일치하는 항목을 찾을 수 없으면 오류를 반환합니다.

1. 미리 보기 요청이 아닌 경우 `UserDomainRefCount` 테이블에서 항목을 삭제합니다.
1. 컴퓨터에 대한 해당 표에 추가 항목이 없으면 항목을 `UserDomainMembership` 삭제하고 [!DNL Key Rollover Required] 속성에 `DomainServerInfo` 플래그를 설정합니다.

각 사용자는 적은 수의 컴퓨터를 등록할 수 있으므로 전체 시스템 ID와 시스템 수를 계산하는 `matches()` 방법을 사용할 수 있습니다. 사용자가 여러 개의 AIR 애플리케이션 또는 여러 브라우저에서 플레이어를 통해 여러 번 등록할 수 있으므로 서버에서는 등록 취소를 카운트할 수 있도록 참조 수를 유지해야 합니다.

>[!NOTE]
>
>컴퓨터의 모든 도메인 토큰이 넘겨질 때까지 등록 해제가 완료되지 않습니다.


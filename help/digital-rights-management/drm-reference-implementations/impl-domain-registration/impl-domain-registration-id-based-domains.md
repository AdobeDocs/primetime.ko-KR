---
title: ID 기반 도메인 등록 논리
description: ID 기반 도메인 등록 논리
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# ID 기반 도메인 등록 논리{#identity-based-domain-registration-logic}

## 도메인 등록 논리 {#section_149C247458954877AF158B4A09A8526B}

참조 구현은 ID 기반 도메인 등록에 대해 다음 논리를 적용합니다.

1. 지정된 사용자에게 할당할 도메인 이름을 결정합니다.

   도메인 이름( `namequalifier:username`)이 인증 토큰에서 추출됩니다. 토큰을 사용할 수 없는 경우 오류가 발생합니다.
1. `DomainServerInfo` 테이블에서 도메인 이름을 찾습니다.

   항목을 찾을 수 없으면 항목을 삽입합니다. 기본값은 다음과 같습니다.

   * `authentication required`
   * `max domain membership=5`

   .

1. 장치가 도메인에 등록되어 있는지 확인하려면:

   1. `UserDomainMembership` 테이블에서 `domainname`을 찾습니다.

      1. 있는 각 컴퓨터 ID에 대해 ID를 요청의 컴퓨터 ID와 비교합니다.
      1. 새 컴퓨터인 경우 `UserDomainMembership` 테이블에 항목을 추가합니다.
      1. `UserDomainRefCount` 테이블에서 일치하는 레코드를 검색합니다.
      1. 이 컴퓨터 GUID에 대한 항목이 없으면 레코드를 추가하십시오.
   1. 새 장치이고 `Max Membership` 값에 도달한 경우 오류를 반환합니다.


1. `DomainKeys` 테이블에서 이 도메인의 모든 도메인 키를 찾습니다.

   1. `DomainServerInfo`이 키를 롤오버해야 한다고 표시되면 새 키 쌍을 생성합니다.
   1. `DomainKeys` 테이블에 쌍을 저장합니다. 이때 가장 높은 기존 키보다 높은 키 버전이 있습니다.
   1. `DomainServerInfo`에서 `Key Rollover Required` 플래그를 재설정합니다.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

## 도메인 등록 취소 논리 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

참조 구현은 ID 기반 도메인 등록 취소에 대해 다음 논리를 적용합니다.

1. 이 사용자에게 할당할 도메인 이름을 결정합니다.

   도메인 이름은 인증 토큰에서 추출되는 `namequalifier:username`입니다. 사용할 수 있는 토큰이 없으면 오류 `DOM_AUTHENTICATION_REQUIRED (503)`을(를) 반환합니다.
1. `DomainServerInfo` 테이블에서 요청된 도메인 이름을 찾습니다.
1. `UserDomainMembership` 테이블에서 도메인 이름을 찾습니다.
1. 찾은 각 컴퓨터 ID를 요청의 컴퓨터 ID와 비교합니다.
1. `UserDomainRefCount` 테이블에서 해당 항목을 찾습니다.

   일치하는 항목이 없으면 오류를 반환합니다.

1. 미리 보기 요청이 아닌 경우 `UserDomainRefCount` 테이블에서 항목을 삭제합니다.
1. 컴퓨터에 대한 해당 표에 추가 항목이 없으면 `UserDomainMembership`에서 항목을 삭제하고 `DomainServerInfo` 속성에 [!DNL Key Rollover Required] 플래그를 설정합니다.

각 사용자는 적은 수의 컴퓨터를 등록할 수 있으므로 전체 컴퓨터 ID와 `matches()` 메서드를 사용하여 컴퓨터를 카운트할 수 있습니다. 사용자는 여러 AIR 응용 프로그램 또는 다른 브라우저에 있는 플레이어를 통해 여러 번 등록할 수 있으므로 등록 취소를 카운트할 수 있도록 참조 카운트를 유지해야 합니다.

>[!NOTE]
>
>컴퓨터의 모든 도메인 토큰이 투항될 때까지 등록 해제가 완료되지 않습니다.


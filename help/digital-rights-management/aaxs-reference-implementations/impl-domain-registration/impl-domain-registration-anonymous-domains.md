---
title: 익명 도메인
description: 익명 도메인
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# 익명 도메인 {#anonymous-domains}

이 경우 많은 수의 디바이스가 단일 도메인에 속해 있으므로 인증이 필요하지 않을 수 있습니다. 참조 구현과 함께 이 유형의 도메인을 사용하려면 도메인 등록이 필수임을 지정하는 정책을 만듭니다. 도메인 서버 URL을 `https:// host:port/flashaccess/domainserver/domainname/`으로 지정하고 익명 인증을 지정합니다.

참조 구현은 도메인 등록에 대한 다음 논리를 구현합니다.

1. 요청 URL에서 도메인 이름을 분석합니다.
1. `DomainServerInfo` 테이블에서 도메인 이름을 조회합니다. 항목을 찾을 수 없으면 표에 항목을 삽입합니다(기본값:인증이 필요하지 않으며 최대 멤버십 수 없음).
1. 요청된 도메인에 대한 인증이 필요한 경우 요청에 유효한 인증 토큰이 포함되어 있는지 확인하고 데이터베이스에 지정된 경우 인증 네임스페이스와 일치시킵니다.

   1. 인증이 필요하지만 유효한 인증 토큰이 제공되지 않은 경우 오류 `DOM_AUTHENTICATION_REQUIRED (503)`을(를) 반환합니다.

1. 장치가 도메인에 이미 등록되어 있는지 확인합니다.

   1. `DomainMembership` 테이블에서 도메인 이름을 조회합니다. 검색된 각 컴퓨터 GUID에 대해 요청의 컴퓨터 GUID와 비교합니다. 새 컴퓨터인 경우 `DomainMembership` 테이블에 항목을 추가합니다.

   1. 새 장치이고 최대 멤버십에 이미 도달한 경우 `DOM_LIMIT_REACHED (502)` 오류를 반환합니다.

1. `DomainKeys` 테이블에서 이 도메인의 모든 도메인 키를 조회합니다.

   1. `DomainServerInfo`이 키를 롤오버해야 한다고 나타내는 경우, 새 키 쌍을 생성하고, `DomainKeys` 테이블에 저장하고(키 버전이 가장 높은 기존 키보다 높음) `DomainServerInfo`에서 `Key Rollover Required` 플래그를 재설정합니다.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

참조 구현은 도메인 등록 취소에 대한 다음 논리를 구현합니다.

1. 요청 URL에서 도메인 이름을 분석합니다.
1. `DomainServerInfo` 테이블에서 요청된 도메인 이름을 조회합니다.
1. 요청된 도메인에 대한 인증이 필요한 경우 요청에 유효한 인증 토큰이 포함되어 있는지 확인하고 데이터베이스에 지정된 경우 인증 네임스페이스와 일치시킵니다.
1. `DomainMembership` 테이블에서 도메인 이름과 컴퓨터 GUID를 조회합니다. 일치하는 항목을 찾을 수 없으면 오류 `DEREG_DENIED (401)`을(를) 반환합니다.

1. 미리 보기 요청이 아닌 경우 `DomainMembership`에서 항목을 삭제하고 `DomainServerInfo`에 `Key Rollover Required` 플래그를 설정합니다.

이 경우 많은 수의 컴퓨터가 도메인에 가입될 수 있으므로 컴퓨터 ID와 완전히 일치시킬 수 없습니다. 대신 개인화 중에 컴퓨터에 할당된 임의 컴퓨터 GUID를 사용합니다.

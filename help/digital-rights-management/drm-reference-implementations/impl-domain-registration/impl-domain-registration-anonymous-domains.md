---
title: 익명 도메인 논리
description: 익명 도메인 논리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 익명 도메인 논리{#anonymous-domain-logic}

## 도메인 등록 논리 {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

참조 구현은 익명 도메인 등록에 대해 다음 논리를 적용합니다.

1. 요청 URL에서 도메인 이름을 구문 분석합니다.
1. 에서 도메인 이름 조회 `DomainServerInfo` 테이블.
1. 항목을 찾을 수 없는 경우 테이블에 항목을 삽입합니다.

   기본값은 다음과 같습니다.

   * `authentication is not required`
   * `no membership maximum`

   요청한 도메인에 인증이 필요한 경우 요청에 유효한 인증 토큰이 있는지 확인하십시오. 데이터베이스에 인증 네임스페이스가 지정된 경우 토큰이 지정된 인증 네임스페이스와 일치해야 합니다.
1. 인증이 필요하지만 유효한 인증 토큰을 사용할 수 없는 경우 오류를 반환합니다 `DOM_AUTHENTICATION_REQUIRED (503)`.
1. 장치가 도메인에 등록되어 있는지 확인합니다.

   1. 에서 도메인 이름 조회 `DomainMembership` 테이블.
   1. 찾은 컴퓨터 GUID를 요청의 컴퓨터 GUID와 비교합니다.
   1. 새 컴퓨터인 경우 `DomainMembership` 테이블.
   1. 새 디바이스 및 `Max Membership` 값에 도달했습니다. 오류 반환 `DOM_LIMIT_REACHED (502)`.

1. 에서 이 도메인의 모든 도메인 키 조회 `DomainKeys` 표:

   1. If `DomainServerInfo` 키를 롤오버해야 함을 나타내며 새 키 쌍을 생성합니다.
   1. 에 키 쌍을 저장합니다. `DomainKeys` 테이블, 가장 높은 기존 키보다 한 숫자 높은 키 버전 사용.
   1. 재설정 `Key Rollover Required` 플래그 `DomainServerInfo`.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

## 도메인 등록 취소 논리 {#section_C968BBFCBFAB4510A903D169F38C9FCE}

참조 구현은 익명 도메인 등록 취소에 대해 다음 논리를 적용합니다.

1. 요청 URL에서 도메인 이름을 구문 분석합니다.
1. 에서 요청된 도메인 이름을 조회합니다. `DomainServerInfo` 테이블.
1. 요청한 도메인에 인증이 필요한 경우 요청에 유효한 인증 토큰이 있는지 확인하십시오.

   토큰은 데이터베이스에 지정된 인증 네임스페이스와 일치해야 합니다.
1. 에서 도메인 이름과 컴퓨터 GUID를 찾습니다. `DomainMembership` 테이블.

   일치하는 항목을 찾을 수 없으면 오류를 반환합니다. `DEREG_DENIED (401)`.

1. 미리 보기 요청이 아닌 경우에서 항목을 삭제합니다. `DomainMembership`, 및 `DomainServerInfo`, 를 설정합니다. `Key Rollover Required` 플래그.

많은 컴퓨터가 도메인에 가입할 수 있으므로 컴퓨터 ID를 일치시킬 수 없습니다. 대신 개별화 중에 컴퓨터에 할당된 임의의 컴퓨터 GUID가 적용됩니다.

---
description: 'null'
seo-description: 'null'
seo-title: 익명 도메인 논리
title: 익명 도메인 논리
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 익명 도메인 논리{#anonymous-domain-logic}

## 도메인 등록 논리 {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

참조 구현은 익명 도메인 등록에 대해 다음 논리를 적용합니다.

1. 요청 URL에서 도메인 이름을 분석합니다.
1. 테이블에서 도메인 이름을 `DomainServerInfo` 찾습니다.
1. 항목을 찾을 수 없는 경우 표에 항목을 삽입합니다.

   기본값은 다음과 같습니다.

   * `authentication is not required`
   * `no membership maximum`
   요청한 도메인에 대한 인증이 필요한 경우 요청에 유효한 인증 토큰이 있는지 확인하십시오. 데이터베이스에 인증 네임스페이스가 지정된 경우 토큰은 지정된 인증 네임스페이스와 일치해야 합니다.
1. 인증이 필요하지만 유효한 인증 토큰을 사용할 수 없는 경우 오류를 `DOM_AUTHENTICATION_REQUIRED (503)`반환합니다.
1. 장치가 도메인에 등록되어 있는지 확인합니다.

   1. 테이블에서 도메인 이름을 `DomainMembership` 찾습니다.
   1. 찾은 컴퓨터 GUID를 요청의 컴퓨터 GUID와 비교합니다.
   1. 새 컴퓨터인 경우 `DomainMembership` 표에 항목을 추가합니다.
   1. 새 장치이고 `Max Membership` 값에 도달한 경우 오류를 반환합니다 `DOM_LIMIT_REACHED (502)`.

1. 다음 `DomainKeys` 표에서 이 도메인에 대한 모든 도메인 키를 찾습니다.

   1. 키를 롤오버해야 `DomainServerInfo` 함을 나타내는 경우 새 키 쌍을 생성합니다.
   1. 키 버전이 가장 높은 기존 키보다 1배 높은 상태로 `DomainKeys` 표에 키 쌍을 저장합니다.
   1. 에서 `Key Rollover Required` 플래그를 재설정합니다 `DomainServerInfo`.

   1. 각 도메인 키에 대해 도메인 자격 증명을 생성합니다.

## 도메인 등록 취소 로직 {#section_C968BBFCBFAB4510A903D169F38C9FCE}

참조 구현은 익명 도메인 등록 취소에 대해 다음 논리를 적용합니다.

1. 요청 URL에서 도메인 이름을 분석합니다.
1. 테이블에서 요청된 도메인 이름을 `DomainServerInfo` 찾습니다.
1. 요청된 도메인에 인증이 필요한 경우 요청에 유효한 인증 토큰이 있는지 확인하십시오.

   토큰은 데이터베이스에 지정된 인증 네임스페이스와 일치해야 합니다.
1. 테이블에서 도메인 이름과 컴퓨터 GUID를 `DomainMembership` 찾습니다.

   일치하는 항목을 찾을 수 없는 경우 오류를 `DEREG_DENIED (401)`반환합니다.

1. 이 요청이 미리 보기 요청이 아닌 경우, 에서 항목을 `DomainMembership`삭제하고 `DomainServerInfo`에서 `Key Rollover Required` 플래그를 설정합니다.

많은 수의 컴퓨터가 도메인에 가입할 수 있으므로 컴퓨터 ID와 일치하면 안 됩니다. 대신 개인 설정 중에 컴퓨터에 할당된 무작위 컴퓨터 GUID가 적용됩니다.

---
description: 'null'
seo-description: 'null'
seo-title: 사용 모델 데모 비즈니스 규칙
title: 사용 모델 데모 비즈니스 규칙
uuid: c55f85be-5ecb-4a78-b47d-7001ec207d3a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 사용 모델 데모 비즈니스 규칙{#usage-model-demo-business-rules}

사용자가 라이센스를 요청하면 참조 구현 서버는 클라이언트가 전송한 메타데이터를 확인하여 `RI_UsageModelDemo` 속성을 사용하여 컨텐츠가 패키지되었는지 확인합니다. 이러한 경우 서버는 다음 비즈니스 규칙을 적용합니다.

* DRM 정책 중 하나에 인증이 필요한 경우:

   * 요청에 유효한 인증 토큰이 들어 있는 경우 고객 데이터베이스 테이블에서 사용자 이름을 검색합니다.

      사용자 이름을 찾을 수 없는 경우 다음 작업을 완료하십시오.

      * 이 `Customer.IsSubscriber` 속성이 `true`*`Subscription`* 로 설정된 경우 사용 모델에 대한 라이선스를 생성하여 사용자에게 전송해야 합니다.

      * 데이터베이스 테이블에서 사용자 이름과 컨텐츠 ID에 대한 레코드를 `CustomerAuthorization` 검색합니다.
      사용자 레코드를 찾을 수 있는 경우 다음 작업을 완료하십시오.

      * 이 `CustomerAuthorization.UsageType` 속성이 로 설정된 `DTO`경우 DTO 사용 모델에 대한 라이선스를 생성하여 사용자에게 전송합니다.

      * 이 `CustomerAuthorization.UsageType` 속성이 로 설정된 `VOD`경우 VOD 사용 모델에 대한 라이선스를 생성하여 사용자에게 전송합니다.
      DRM 정책 중 익명 액세스를 허용하지 않는 경우 다음 작업을 완료하십시오.

      * 요청에 유효한 인증 토큰이 없는 경우 &quot;인증 필수&quot; 오류를 반환해야 합니다.
      * 그렇지 않으면 &quot;인증되지 않음&quot; 오류를 반환합니다.



* DRM 정책 중 하나가 익명 액세스를 허용하는 경우 광고 기금 사용 모델에 대한 라이선스를 생성하여 사용자에게 보냅니다.


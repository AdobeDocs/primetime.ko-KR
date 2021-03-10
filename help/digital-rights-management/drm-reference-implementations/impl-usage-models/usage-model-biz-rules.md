---
title: 사용 모델 데모 비즈니스 규칙
description: 사용 모델 데모 비즈니스 규칙
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 사용량 모델 데모 비즈니스 규칙{#usage-model-demo-business-rules}

사용자가 라이선스를 요청하면 참조 구현 서버는 클라이언트가 보낸 메타데이터를 확인하여 `RI_UsageModelDemo` 속성을 사용하여 컨텐츠가 패키지되었는지 확인합니다. 이 경우 서버는 다음 비즈니스 규칙을 적용합니다.

* DRM 정책 중 하나에 인증이 필요한 경우:

   * 요청에 유효한 인증 토큰이 들어 있으면 고객 데이터베이스 테이블에서 사용자 이름을 검색합니다.

      사용자 이름을 찾을 수 없는 경우 다음 작업을 완료하십시오.

      * `Customer.IsSubscriber` 속성이 `true`으로 설정된 경우 *`Subscription`* 사용 모델에 대한 라이선스를 생성하여 사용자에게 보내야 합니다.

      * 사용자 이름과 콘텐트 ID에 대한 레코드를 `CustomerAuthorization` 데이터베이스 테이블에서 검색합니다.

      사용자의 레코드를 찾을 수 있는 경우 다음 작업을 완료하십시오.

      * `CustomerAuthorization.UsageType` 속성이 `DTO`로 설정된 경우 DTO 사용 모델에 대한 라이센스를 생성하여 사용자에게 전송합니다.

      * `CustomerAuthorization.UsageType` 속성이 `VOD`로 설정된 경우 VOD 사용 모델에 대한 라이선스를 생성하여 사용자에게 전송합니다.

      DRM 정책 중 익명 액세스를 허용하는 것이 없으면 다음 작업을 완료하십시오.

      * 요청에 유효한 인증 토큰이 없는 경우 &quot;인증 필수&quot; 오류를 반환해야 합니다.
      * 그렇지 않으면 &quot;인증되지 않음&quot; 오류를 반환합니다.



* DRM 정책 중 하나가 익명 액세스를 허용하는 경우 광고 기금 사용 모델에 대한 라이선스를 생성하여 사용자에게 전송합니다.


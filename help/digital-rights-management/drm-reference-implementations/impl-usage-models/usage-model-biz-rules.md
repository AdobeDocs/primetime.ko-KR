---
title: 사용 모델 데모 비즈니스 규칙
description: 사용 모델 데모 비즈니스 규칙
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 사용 모델 데모 비즈니스 규칙{#usage-model-demo-business-rules}

사용자가 라이선스를 요청하면 참조 구현 서버는 클라이언트가 보낸 메타데이터를 확인하여 콘텐츠가 `RI_UsageModelDemo` 속성. 이 경우 서버는 다음 비즈니스 규칙을 적용합니다.

* DRM 정책 중 하나에 인증이 필요한 경우:

   * 요청에 유효한 인증 토큰이 포함된 경우 고객 데이터베이스 테이블에서 사용자 이름을 검색합니다.

     사용자 이름을 찾을 수 없는 경우 다음 작업을 완료하십시오.

      * 다음과 같은 경우 `Customer.IsSubscriber` 속성이 로 설정되어 있습니다. `true`, 다음에 대한 라이선스를 생성해야 합니다. *`Subscription`* 사용 모델을 생성하여 사용자에게 보냅니다.

      * 에서 레코드 검색 `CustomerAuthorization` 사용자 이름 및 컨텐츠 ID에 대한 데이터베이스 테이블.

     사용자 레코드를 찾을 수 있는 경우 다음 작업을 완료하십시오.

      * 다음과 같은 경우 `CustomerAuthorization.UsageType` 속성이 로 설정되어 있습니다. `DTO`를 통해 DTO 사용 모델에 대한 라이선스를 생성하여 사용자에게 보냅니다.

      * 다음과 같은 경우 `CustomerAuthorization.UsageType` 속성이 로 설정되어 있습니다. `VOD`, VOD 사용 모델에 대한 라이선스를 생성하여 사용자에게 보냅니다.

     익명 액세스를 허용하는 DRM 정책이 없는 경우 다음 작업을 완료하십시오.

      * 요청에 유효한 인증 토큰이 없으면 &quot;인증 필수&quot; 오류를 반환해야 합니다.
      * 그렇지 않으면 &quot;승인되지 않음&quot; 오류를 반환합니다.

* DRM 정책 중 하나에서 익명 액세스를 허용하는 경우 광고 지원 사용 모델에 대한 라이선스를 생성하여 사용자에게 보냅니다.

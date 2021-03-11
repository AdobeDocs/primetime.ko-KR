---
title: 사용 모델 구현 개요
description: 사용 모델 구현 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# 사용 모델 구현 개요 {#implementing-the-usage-models-overview}

참조 구현에는 패키지된 컨텐츠 조각에 대해 다음 4개의 서로 다른 사용 모델을 사용하는 방법을 시연하기 위한 비즈니스 로직이 포함되어 있습니다.

* DTO(Download-to-Own)
* 대여/주문형 비디오(VOD)
* 구독(모두 사용 가능)
* 광고 지원

사용 모델 데모를 활성화하려면 패키징 시 사용자 지정 속성 `RI_UsageModelDemo=true`을(를) 지정합니다. Media Packager 명령줄 도구를 사용하여 내용을 패키지하는 경우 다음을 지정합니다.

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>패키징 시 선택적 데모 모드를 활성화하지 않는 경우 라이선스 서버는 패키징 시 지정된 정책을 사용하여 라이선스를 발행합니다. 여러 정책을 지정한 경우 라이선스 서버는 첫 번째 유효한 정책을 사용합니다.

데모에서는 서버의 비즈니스 논리가 생성된 라이선스의 실제 속성을 제어합니다. 패키징 시 컨텐츠에 최소 정책 정보만 포함되어야 합니다. 특히 정책에 따라 콘텐츠에 액세스하려면 인증이 필요한지 여부를 표시해야 합니다. 4개의 사용 모델을 모두 활성화하려면(광고 기금 지원 모델의 경우) 익명 액세스를 허용하는 하나의 정책과 사용자 이름/암호 인증이 필요한 정책(다른 3개의 사용 모델의 경우)을 포함합니다. 라이센스를 요청할 때 클라이언트 응용 프로그램은 정책의 인증 정보를 기반으로 사용자에게 인증을 요청할지 여부를 결정할 수 있습니다.

특정 사용자에게 라이선스를 부여할 사용 모델을 제어하기 위해 항목을 참조 구현 데이터베이스에 추가할 수 있습니다. `Customer` 테이블에는 사용자를 인증하기 위한 사용자 이름과 암호가 포함되어 있습니다. 사용자에게 구독이 있는지 여부도 표시됩니다. 구독이 있는 사용자는 *구독* 사용 모델에 따라 라이선스를 받게 됩니다. *Download to Own* 또는 *Video on Demand* 사용 모델에서 사용자에게 액세스 권한을 부여하기 위해 사용자가 액세스할 수 있는 각 컨텐트 및 사용 모델을 지정하는 항목을 `CustomerAuthorization` 테이블에 추가할 수 있습니다. 각 표 채우기에 대한 자세한 내용은 [!DNL PopulateSampleDB.sql] 스크립트를 참조하십시오.

사용자가 라이선스를 요청하면 참조 구현 서버는 클라이언트가 보낸 메타데이터를 확인하여 컨텐츠가 `RI_UsageModelDemo` 속성을 사용하여 패키지되었는지 확인합니다. 이 경우 다음 비즈니스 규칙이 사용됩니다.

* 정책 중 하나에 인증이 필요한 경우:

   * 요청에 유효한 인증 토큰이 들어 있으면 고객 데이터베이스 테이블에서 사용자를 찾습니다. 사용자를 찾은 경우:

      * `Customer.IsSubscriber` 속성이 `true`인 경우 *구독* 사용 모델에 대한 라이선스를 생성하여 사용자에게 보냅니다.

      * 이 사용자 및 콘텐트 ID에 대한 `CustomerAuthorization` 데이터베이스 테이블에서 레코드를 찾습니다. 레코드를 찾은 경우:

         * `CustomerAuthorization.UsageType`이(가) `DTO`인 경우 *직접 다운로드* 사용 모델에 대한 라이센스를 생성하여 사용자에게 보냅니다.

         * `CustomerAuthorization.UsageType`이(가) `VOD`인 경우 *Video On Demand* 사용 모델에 대한 라이선스를 생성하여 사용자에게 보냅니다.
   * 정책에서 익명 액세스를 허용하지 않는 경우:

      * 요청에 유효한 인증 토큰이 없는 경우 &quot;인증 필요&quot; 오류를 반환합니다.
      * 그렇지 않으면 &quot;인증되지 않음&quot; 오류를 반환합니다.


* 정책 중 하나가 익명 액세스를 허용하는 경우 광고 기금 사용 모델에 대한 라이선스를 생성하여 사용자에게 전송합니다.

참조 구현 서버에서 사용 모델 데모의 라이센스를 발급하려면 먼저 4개의 사용 모델 각각에 대해 라이센스가 생성되는 방법을 지정하도록 서버를 구성해야 합니다. 이 작업은 각 사용 모델에 대한 정책을 지정하여 수행합니다. 참조 구현에는 4개의 샘플 정책( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol])이 포함되어 있거나 사용자 고유의 정책으로 대체할 수 있습니다. [!DNL flashaccess-refimpl.properties]에서 다음 속성을 설정하여 각 사용 모델에 사용할 정책을 지정하고 정책 파일을 `config.resourcesDirectory` 속성에 지정된 디렉토리에 넣습니다.

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```


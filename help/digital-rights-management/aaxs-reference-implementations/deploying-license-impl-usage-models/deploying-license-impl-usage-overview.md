---
title: 사용 모델 구현 개요
description: 사용 모델 구현 개요
copied-description: true
exl-id: 48e7db54-484f-4c46-9a4e-a51bae7c84b4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 사용 모델 구현 개요 {#implementing-the-usage-models-overview}

참조 구현에는 패키지된 콘텐츠 하나에 대해 다음 4가지 다른 사용 모델을 활성화하는 방법을 보여 주는 비즈니스 논리가 포함되어 있습니다.

* DTO(다운로드 소유)
* 렌탈/주문형 비디오(VOD)
* 구독(무한 리필)
* 광고 지원됨

사용 모델 데모를 활성화하려면 사용자 지정 속성을 지정합니다 `RI_UsageModelDemo=true` 포장 시간에. Media Packager 명령줄 도구를 사용하여 콘텐츠를 패키지하는 경우 다음을 지정합니다.

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>패키징 시간에 선택적 데모 모드를 활성화하지 않을 경우 라이센스 서버는 패키징 시간에 지정된 정책을 사용하여 라이센스를 발행합니다. 여러 정책을 지정한 경우 라이선스 서버는 첫 번째 유효한 정책을 사용합니다.

데모에서는 서버의 비즈니스 로직이 생성된 라이센스의 실제 속성을 제어합니다. 패키징 타임에는 최소한의 정책정보만이 그 내용에 포함되어야 한다. 특히 콘텐츠에 액세스하기 위해 인증이 필요한지 여부만 정책에 표시하면 됩니다. 4개의 사용 모델을 모두 활성화하려면 익명 액세스를 허용하는 정책(광고 지원 모델의 경우)과 사용자 이름/암호 인증이 필요한 정책(다른 3개의 사용 모델의 경우)을 모두 포함하십시오. 라이센스를 요청할 때 클라이언트 애플리케이션은 정책의 인증 정보를 기반으로 사용자에게 인증을 요구할지 여부를 결정할 수 있습니다.

특정 사용자에게 라이센스가 부여되는 사용 모델을 제어하기 위해 참조 구현 데이터베이스에 항목이 추가될 수 있습니다. 다음 `Customer` 표에는 사용자 인증을 위한 사용자 이름과 암호가 포함되어 있습니다. 또한 사용자에게 구독이 있는지 여부도 표시됩니다. 구독이 있는 사용자는 *구독* 사용 모델. 사용자에게 액세스 권한을 부여하려면 *소유로 다운로드* 또는 *Video on Demand* 사용 모델, 항목에 항목 추가 가능 `CustomerAuthorization` 테이블 - 사용자가 액세스할 수 있는 각 콘텐츠 및 사용 모델을 지정합니다. 다음을 참조하십시오. [!DNL PopulateSampleDB.sql] 각 테이블 채우기에 대한 자세한 내용은 스크립트를 참조하십시오.

사용자가 라이선스를 요청하면 참조 구현 서버는 클라이언트가 보낸 메타데이터를 확인하여 콘텐츠가 `RI_UsageModelDemo` 속성. 이 경우 다음 비즈니스 규칙이 사용됩니다.

* 정책 중 하나에 인증이 필요한 경우:

   * 요청에 유효한 인증 토큰이 포함된 경우 고객 데이터베이스 테이블에서 사용자를 찾습니다. 사용자를 찾은 경우:

      * 다음과 같은 경우 `Customer.IsSubscriber` 속성은 입니다. `true`, 다음에 대한 라이선스 생성 *구독* 사용 모델을 생성하여 사용자에게 보냅니다.

      * 에서 레코드 찾기 `CustomerAuthorization` 이 사용자 및 콘텐츠 ID에 대한 데이터베이스 테이블입니다. 레코드가 발견된 경우:

         * If `CustomerAuthorization.UsageType` 은(는) `DTO`, 다음에 대한 라이선스 생성 *소유로 다운로드* 사용 모델을 생성하여 사용자에게 보냅니다.

         * If `CustomerAuthorization.UsageType` 은(는) `VOD`, 다음에 대한 라이선스 생성 *Video On Demand* 사용 모델을 생성하여 사용자에게 보냅니다.
   * 익명 액세스를 허용하는 정책이 없는 경우:

      * 요청에 유효한 인증 토큰이 없으면 &quot;인증 필수&quot; 오류를 반환합니다.
      * 그렇지 않으면 &quot;승인되지 않음&quot; 오류를 반환합니다.


* 정책 중 하나에서 익명 액세스를 허용하는 경우 광고 자금 사용 모델에 대한 라이선스를 생성하여 사용자에게 보냅니다.

참조 구현 서버에서 사용 모델 데모에 대한 라이선스를 발급하려면 먼저 4개의 사용 모델 각각에 대해 라이선스가 생성되는 방법을 지정하도록 서버를 구성해야 합니다. 이는 각 사용 모델에 대한 정책을 지정하여 수행됩니다. 참조 구현에는 네 가지 샘플 정책( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) 또는 자신의 정책을 대체할 수 있습니다. 위치 [!DNL flashaccess-refimpl.properties]를 클릭하고 다음 속성을 설정하여 각 사용 모델에 사용할 정책을 지정하고 정책에서 지정한 디렉터리에 정책 파일을 저장합니다. `config.resourcesDirectory` 속성:

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

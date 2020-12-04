---
seo-title: 참조 구현 DB 업데이트
title: 참조 구현 DB 업데이트
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 참조 구현 DB{#update-the-reference-implementation-db} 업데이트

지정된 사용자에게 라이센스가 발급되는 사용 모델을 제어하려면 참조 구현 데이터베이스에 항목을 추가합니다.

1. `Customer` 테이블에 항목을 추가합니다.

   `Customer` 표에는 사용자를 인증하기 위한 사용자 이름과 암호가 포함되어 있습니다. 또한 사용자에게 구독(*구독* 사용 모델에 따라 발행된 라이센스)이 있는지 여부도 표시됩니다.

1. 사용자에게 직접 다운로드 또는 VOD(Video-On-Demand) 사용 모델 아래에 액세스 권한을 부여합니다.

       &#39;CustomerAuthorization&#39; 테이블에 항목을 추가하여 다음을 지정합니다.
   
   * 사용 모델
   * 사용자가 액세스할 수 있는 각 컨텐츠 세그먼트

각 테이블을 채우는 방법에 대한 자세한 내용은 [!DNL PopulateSampleDB.sql] 스크립트([!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] 디렉토리의 Primetime DRM DVD에 포함)를 참조하십시오.

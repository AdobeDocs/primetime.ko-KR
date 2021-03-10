---
title: 참조 구현 DB 업데이트
description: 참조 구현 DB 업데이트
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 참조 구현 DB{#update-the-reference-implementation-db} 업데이트

지정된 사용자에게 라이센스가 발급되는 사용 모델을 제어하려면 참조 구현 데이터베이스에 항목을 추가합니다.

1. `Customer` 테이블에 항목을 추가합니다.

   `Customer` 표에는 사용자를 인증하기 위한 사용자 이름과 암호가 포함되어 있습니다. 사용자에게 구독(*구독* 사용 모델에 의해 발급된 라이센스)이 있는지 여부도 표시됩니다.

1. 사용자에게 직접 다운로드 또는 VOD(Video-On-Demand) 사용 모델에서 액세스 권한을 부여합니다.

       &#39;CustomerAuthorization&#39; 테이블에 항목을 추가하여 다음을 지정합니다.
   
   * 사용 모델
   * 사용자가 액세스할 수 있는 각 컨텐츠 세그먼트

각 표를 채우는 방법에 대한 자세한 내용은 [!DNL PopulateSampleDB.sql] 스크립트([!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] 디렉토리의 Primetime DRM DVD에 포함)를 참조하십시오.

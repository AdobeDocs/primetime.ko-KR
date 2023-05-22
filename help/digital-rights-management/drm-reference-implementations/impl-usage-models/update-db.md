---
title: 참조 구현 DB 업데이트
description: 참조 구현 DB 업데이트
copied-description: true
exl-id: b337bf9c-7add-47b8-9576-db7fa067c51d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 참조 구현 DB 업데이트{#update-the-reference-implementation-db}

지정된 사용자에게 라이센스를 발급하는 사용 모델을 제어하려면 참조 구현 데이터베이스에 항목을 추가합니다.

1. 에 항목 추가 `Customer` 테이블.

   다음 `Customer` 표에는 사용자를 인증하기 위한 사용자 이름과 암호가 포함되어 있습니다. 또한 사용자에게 구독(아래에 발급된 라이선스)이 있는지 여부도 표시됩니다. *구독* 사용 모델)을 참조하십시오.

1. 사용자에게 Download-to-own 또는 Video-on-demand 사용 모델에 대한 액세스 권한을 부여합니다.

       &#39;CustomerAuthorization&#39; 테이블에 항목을 추가하여 다음을 지정합니다.
   
   * 사용 모델
   * 사용자가 액세스할 수 있는 컨텐츠의 각 세그먼트

각 테이블을 채우는 방법에 대한 자세한 내용은 [!DNL PopulateSampleDB.sql] 스크립트(의 Primetime DRM DVD에 포함됨) [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] directory).

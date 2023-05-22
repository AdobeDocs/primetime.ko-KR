---
description: TVSDK는 Adobe Primetime ad decisioning과 같은 광고 게재 서비스에 연결하고 광고 비디오 스트림에 해당하는 기본 재생 목록 파일을 가져오려고 합니다. 광고 해결 단계 동안 TVSDK는 원격 광고 전달 서버에 대한 HTTP 호출을 수행하고 서버의 응답을 구문 분석합니다.
title: 광고 해결 단계
exl-id: 5dd96709-1a65-442f-a753-a4343c6e8762
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 광고 해결 단계{#ad-resolving-phase}

TVSDK는 Adobe Primetime ad decisioning과 같은 광고 게재 서비스에 연결하고 광고 비디오 스트림에 해당하는 기본 재생 목록 파일을 가져오려고 합니다. 광고 해결 단계 동안 TVSDK는 원격 광고 전달 서버에 대한 HTTP 호출을 수행하고 서버의 응답을 구문 분석합니다.

TVSDK는 다음 유형의 광고 공급자를 지원합니다.

* 메타데이터 광고 공급자

   광고 데이터는 일반 텍스트 JSON 파일로 인코딩됩니다.
* Primetime ad decisioning 광고 공급자

   TVSDK가 타겟팅 매개 변수 세트와 자산 식별 번호를 포함하는 요청을 Primetime ad decisioning 백엔드 서버로 전송합니다. Primetime ad decisioning 은 필수 광고 정보가 포함된 SMIL(Synchronized Multimedia Integration Language) 문서에 응답합니다.
* 사용자 지정 광고 마커 공급자

   광고가 서버 측에서 스트림으로 연소되는 상황을 처리합니다. TVSDK는 실제 광고 삽입을 수행하지 않지만 서버측에 삽입된 광고를 추적해야 합니다. 이 공급자는 TVSDK가 광고 추적을 수행하는 데 사용하는 광고 마커를 설정합니다.

이 단계에서 다음 페일오버 상황 중 하나가 발생할 수 있습니다.

* 리소스가 없는 등의 연결 결여 또는 서버측 오류 등의 이유로 데이터를 검색할 수 없습니다.
* 데이터가 검색되었지만 형식이 잘못되었습니다.

   예를 들어 인바운드 데이터의 구문 분석이 실패했기 때문에 이러한 문제가 발생할 수 있습니다.

TVSDK에서 오류에 대한 경고 알림을 보내고 처리를 계속합니다.

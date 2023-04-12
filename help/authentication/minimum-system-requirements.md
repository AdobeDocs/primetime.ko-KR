---
title: 최소 시스템 요구 사항
description: 최소 시스템 요구 사항
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# 최소 시스템 요구 사항 {#minimum-system-requirements}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.


## 개요 {#overview}

이 문서에서는 지원되는 플랫폼에서 Adobe Primetime 인증 통합을 구현하기 위한 현재 소프트웨어 및 하드웨어 요구 사항을 설명합니다. 아래에 나열된 지원되는 모든 웹/모바일 브라우저 및 운영 체제는 합의된 SLA에 따라 Adobe Primetime 인증 팀을 완벽하게 지원합니다.

Adobe Primetime 인증 팀에서는 최신 안정된 버전의 브라우저 및 운영 체제를 사용하는 것을 권장합니다. 또한 adobe는 현재 사용 중인 비호환/이전 플랫폼 및 브라우저의 존재 여부를 확인합니다. 이러한 오래된 장치들은 여전히 문제 없이 작동할 수도 있지만, 더 오류가 발생하기 쉽습니다.

이러한 오래된 플랫폼에 나타나는 문제를 완화하는 초기 접근 방식은 최신 버전으로 업그레이드해야 합니다. OS 버전, 브라우저 버전 또는 설치된 애플리케이션 버전일 수 있습니다.

이러한 플랫폼에 나타나는 모든 문제는 Adobe Primetime 인증 팀이 최선을 다해 해결됩니다. 

Adobe Primetime은 고객 및 파트너가 성능, 효율성 및 보안 개선 사항 외에 잠재적인 문제에 대한 Adobe의 완벽한 지원을 통해 최신 버전으로 업그레이드하는 것을 고려해 볼 것을 권장합니다. 


## 브라우저 및 운영 체제 요구 사항 {#browser-OS-system-requirements}


| 웹/모바일 브라우저(†) | 지원되는 버전 |
|---|---|
| Google Chrome | **70** 또는 나중에 |
| Mozilla Firefox | **57** 또는 나중에 |
| Apple Safari | **14** 또는 나중에 |
| Microsoft Edge | **100년** 또는 나중에 |

(†) Adobe은 비공개 모드나 시크릿 모드를 사용하지 않도록 권장합니다.

| 운영 체제 | 지원되는 버전 |
|---|---|
| *Android* | **7.0** (Nougat) 이상 |
| *iOS* | **14** 또는 나중에 |
| *iPadOS* | **14** 또는 나중에 |
| *tvOS* | **14** 또는 나중에 |
| *Fire OS* | **5(Android 5.1)** 또는 나중에 |
| *Mac OS* | **10.13** 또는 나중에 |
| *Microsoft Windows* | **10** 또는 나중에 |




>[!NOTE]
>
>타사 쿠키 - 타사 쿠키를 비활성화하면 Adobe Primetime 인증 자격 흐름이 실패할 수 있습니다.  이 문제는 브라우저 설정이 수정될 때만 재생됩니다. 지원되는 모든 브라우저의 경우 Primetime 인증이 기본 설정으로 작동해야 합니다.\
 

## Clientless(REST) 구현을 위한 장치 요구 사항 {#general_clientless_reqs}

 
클라이언트 없는 구현을 통해 Adobe Primetime 인증 서비스를 사용하는 모든 장치 **다음을 수행할 수 있어야 합니다.**:

* 해시된 고유한 장치 ID를 제공합니다. 장치에서 고유한 해시된 장치 ID를 제공하지 않는 경우 Adobe Primetime 인증에서 제공한 고유 ID를 유지할 수 있어야 합니다. 장치는 로컬 저장소에서 고유 ID를 영구적으로 유지하고 Adobe Primetime 인증 API를 호출할 때 장치 ID로서 고유 ID를 제공할 수 있어야 합니다.
* HMAC-SHA1 알고리즘을 사용하여 디지털 서명 생성
* 임의 HTTP 헤더 설정
* RESTful 웹 서비스 사용
* XML 및 JSON 데이터 형식을 구문 분석합니다
* HTTPS를 사용하여 트래픽 보내기
* HTTP 오류 코드 처리

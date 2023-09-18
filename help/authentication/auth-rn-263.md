---
title: Adobe Primetime 인증 2.63 릴리스 노트
description: Adobe Primetime 인증 2.63 릴리스 노트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Adobe Primetime Authentication 2.63 릴리스 노트 {#pt-authn-263-rn}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

이 페이지에서는 이 릴리스의 새로운 기능, 변경 사항 및 알려진 문제에 대해 설명합니다.

## 서버측 및 웹 클라이언트 {#server-side-web-clients-263}

* [빌드 번호](#build-number)
* [새로운 기능](#new-features)

### 빌드 번호 {#build-number-263}

Adobe Primetime 인증: adobe-pass-**2.63**
릴리스 날짜: **2022년 9월 20일 - 2022년 9월 22일**

### 새로운 기능 {#new-features-263}

#### 플랫폼 식별 메커니즘 개선 {#pf-identification-mech}

* 이 릴리스부터 디바이스를 식별하는 데 사용되는 메커니즘을 개선했으며 더 이상 클라이언트측 구현에 종속되지 않습니다. 이렇게 하면 플랫폼 수준에서 비즈니스 규칙을 적용할 때 더 정확한 세부기간을 제공할 수 있고 ESM 보고서의 트래픽 값에 대한 더 나은 이해를 제공할 수 있습니다.

* 플랫폼 관련 필드를 표시하는 새롭고 개선된 보고서와 함께 새로운 ESM 릴리스가 곧 제공될 예정입니다.

* 계획된 변경 사항에 대한 자세한 내용은 TAM에 문의하십시오.

#### MVPD 자가 저하 {#mvpd-self-degradation}

이 기능은 MVPD에 각 종단점에 대한 로드가 너무 커지면 높은 트래픽 시나리오에 대해 자체 인증 및 권한 부여 종단점을 일시적으로 우회하는 기능을 제공합니다.


#### 인증 호출 헤더에 프록시화된 ID 추가 {#add-proxied-id}

이 기능은 인증 호출의 헤더에 Synacor 프록시화된 MVPD의 ID를 추가합니다. 이를 통해 Synacor는 각 개별 프록시에 대한 비즈니스 규칙을 설정할 수 있습니다(예: 프록시화된 MVPD별로 다른 도메인으로 라우팅).


#### TVE 대시보드 {#tve-dashboard}

이 릴리스에서는 MVPD 수준에서 authN 또는 authZ TTL 집합이 구성 보고서에서 올바르게 계산되지 않는 문제를 해결했습니다.


#### JavaScript SDK 4.6.0 {#js-sdk}

* 의 사용을 제거했습니다. `eval` 를 사용하여 SDK가 컨텐츠 보안 정책을 준수하도록 할 수 있습니다.
* 파트너 애플리케이션에서 브라우저의 로컬 스토리지를 명시적으로 삭제했을 때 인증 흐름이 정상적으로 완료되지 않는 문제를 해결했습니다.

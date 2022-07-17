---
title: 계정 IQ 용어집
description: '제품 용어 목록.  '
source-git-commit: 8d8aa00d693b1ca7f960a71b40053e47249c63e4
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# 제품 개념 및 용어집 {#glossary}

다음 제품 용어 및 해당 정의를 참조하십시오.

## 계정 공유 가능성 {#account-sharing-probability-def}

점수를 공유하는 현재 세그먼트를 매우 낮음, 낮음, 보통, 높음 및 매우 높음의 범위 카테고리로 나누는 차트로 표시하는 대시보드 패널입니다.

## 작업 {#action-def}

와 연결된 직접 또는 간접 이벤트 [작업](#operation-def) 관련 작업 세그먼트(또는 집단)의 특성(예: 공유 점수 또는 사용 중인 장치 수)에 영향을 줍니다.

## 집계된 공유 점수 {#sharing-probability-level-def}

점수를 공유하는 현재 세그먼트를 매우 낮음, 낮음, 보통, 높음 및 매우 높음의 범위 카테고리로 나누는 차트로 나누고, 세그먼트에 대한 전체 스트리밍 금액의 각 카테고리 백분율과 함께 대시보드 패널입니다.

## AuthN {#authn-def}

인증 또는 인증 시도 횟수. 인증 시도는 현재 유효한 인증 상태가 없는 사용자가 선택된 MVPD로 리디렉션되는 프로세스입니다. 여기서 사용자는 MVPD로 식별됩니다(일반적으로 사용자 이름과 암호로).

## AuthN 확인 {#authn-ok-def}

성공한 인증 수입니다. 성공적인 인증은 MVPD에 의해 사용자가 식별되고 사용자가 다시 프로그래머 앱 또는 사이트로 리디렉션될 때 발생합니다.

## AuthZ {#authz-def}

권한 부여 또는 권한 부여 요청 수. 권한 부여 요청은 프로그래머가 Adobe을 통해 MVPD로부터 사용자 요청된 콘텐츠를 스트리밍하기 위한 권한을 요청하는 프로세스입니다. MVPD는 일반적으로 사용자의 MVPD 구독과 연결된 컨텐츠 권한(예: 컨텐츠와 연결된 채널이 사용자의 구독에 있는지 여부)을 기반으로 요청을 부여합니다. 일부 인증 요청 응답은 Adobe에 의해 캐시되므로 Adobe이 MVPD에 요청을 전달하지 않고 즉시 응답할 수 있습니다.

## AuthZ 확인 {#authz-ok-def}

성공한 권한 수.

## 채널 {#channel-def}

Channel 은 속성도 알고 있는 비디오 컨텐츠의 테마 관련 소스입니다. 일반적으로 MVPD의 고유한 숫자 지정 가능한 연속 비디오 피드를 나타냅니다. 이 채널은 STB(Set Top Box)를 통해 구독자가 사용할 수 있는 액세스 가능한 컨텐츠 채널에 직접 매핑됩니다.

## 클러스터 {#cluster-def}

클러스터는 위치 및 장치의 컬렉션입니다. 클러스터는 장치 간에 공통 위치를 찾아 생성합니다. 공통 위치에 표시된 장치는 동일한 클러스터에 속하는 것으로 간주됩니다. 두 장치는 공통 위치가 없어도 동일한 클러스터에 있을 수 있지만 다른 장치의 위치를 통해 연결할 수 있습니다.

### 모바일 클러스터 {#mobile-cluster-def}

정적 장치가 없는 클러스터입니다.

### 정적 클러스터 {#static-cluster-def}

정적 장치가 하나 이상 있는 클러스터.

## 동시 실행 {#consurrency-def}

동시에 또는 매우 가까운 시간에 재생되는 두 개 이상의 스트림에 의해 정의되므로 정상적인 속도로 이동함으로써 두 스트림 사이의 간격을 정당화할 수 없습니다.
동시 사용량은 두 개의 다른 클러스터 사이의 최대 속도(마일/시간)를 사용하여 계산됩니다. 124마일 미만의 거리에서 124m/h보다 큰 속도를 가지고 있거나 124마일 이상의 거리에서 400m/h보다 큰 속도를 가진 사용자는 동시 사용을 하는 것으로 간주됩니다. 거리는 서로 다른 클러스터의 위치 간에 계산됩니다. 동일한 클러스터에서 동시 사용이 허용됩니다.

## 장치 {#device-def}

TV Everywhere 컨텐츠를 재생할 수 있고 Adobe Pass에서 지원하는 디지털 비디오 하드웨어 제품. 예를 들어, 스마트폰, 노트북 및 데스크탑 컴퓨터, 게임 콘솔 및 스마트 TV가 있습니다.

## 지리 범위 {#geographical-span-def}

위치 집합에서 가장 먼 점 사이의 거리.

## 세부기간 {#granularity-def}

기간 과 관련하여 마침표의 크기 1주 또는 1개월 등.

## 업계 평균 지수 {#industry-avg-index-def}

선택한 기간 동안 모든 프로그래머 및 MVPD에서 각 위험 지표(계정, 사용, 전체)에 대해 계산된 값입니다.

## IP {#ip-def}

인터넷 서비스 공급자가 장치에 할당한 인터넷 프로토콜 주소입니다. 예를 들어, 케이블 서비스 공급자 및 셀 서비스 공급자가 있습니다.

## 격리 모드 {#isolation-mode-def}

계정 평가가 선택한 세그먼트의 프로그래머에게 직접 발생한 이벤트로 제한되는 공유 분석 유형입니다.  일반적으로 모든 계정 이벤트가 평가되며, 이를 통해 더 정확한 공유 추정값을 제공합니다.  일부 MVPD 데이터는 격리 모드 분석만 허용하는 방식으로 구성되어 있습니다.

## 위치 {#location-def}

지구 상의 독특한 점. 또한 Pass 데이터를 사용하여 감지된 특정 재생 요청의 지리적 위치라고도 하며, 정밀도가 1000mx1000m(1제곱 km)입니다.

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## 미디어 회사 {#media-company-def}

미디어 회사는 미디어 네트워크 그룹을 소유하는 회사입니다.

## 지표 {#metric}

지표는 가입자 계정의 속성입니다(예: 해당 MVPD, 프로그래머 및 스트림 컨텐츠의 채널, 사용하는 장치 수).

## 모바일 장치 {#mobile-device-def}

이동성이 높은 장치. 예를 들어, 휴대폰 및 태블릿이 있습니다.

## MVPD {#mvpd-def}

배포자라고도 하는 MVPD는 Media Company 비디오 컨텐츠의 누적, 리셀러 및 배포자입니다.

## 작업 {#operation-def}

작업은 특정 작업의 효과를 추적하기 위해 만들어진 레코드입니다 [작업](#action-def) 연결된 세그먼트에 있을 수 있습니다. 작업의 예는 세그먼트로 식별된 계정에 대해 허용되는 동시 스트림 수에 제한이 될 수 있습니다.

## 전체 공유 점수 {#overall-sharing-score}

사용자가 프로그래머 속성 또는 MVPD 구독자에 대한 암호 공유의 크기를 이해하고 사용자에게 즉시 사용할 수 있는 긴급성을 제공하는 값입니다.

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## 재생 요청 {#play-requests-def}

스트림 시작을 기록하고 보호하기 위해 미디어 토큰을 요청하기 위해 클라이언트 앱 또는 사이트에서 Adobe을 요청하는 요청입니다.

## 프로그래머 {#programmer-def}

Network라고도 하는 프로그래머는 하나 이상의 채널을 소유하고 관리하는 대기업(기업)의 자회사인 회사입니다.

## requestorID {#requestorid-def}

미디어 회사가 자신을 식별하는 데 사용하는 ID 또는 MVPD에 대한 자회사를 식별합니다.  프로그래머 구현에 따라 미디어 회사, 프로그래머 또는 채널에 매핑될 수 있습니다.  미디어 회사가 자신을 식별하거나 MVPD에 대한 자회사를 식별하는 데 사용하는 가장 일반적인 ID입니다.  프로그래머 구현에 따라 미디어 회사, 프로그래머 또는 채널에 매핑될 수 있습니다.  일반적으로 채널에 매핑됩니다.  MML(March Wurnize Live)과 같은 의사 채널을 만들고 기술적으로 MVPD 기반 데이터 제한 사항을 해결하기 위해 이동하면서 requestorID는 미디어 회사와 더욱 연관되기 시작하고 있습니다.

## resourceID {#resource-id-def}

최종 사용자가 요청한 콘텐츠입니다.  일반적으로 이는 사용자가 요청한 콘텐츠와 연결된 채널을 식별했습니다.  시스템 개선 사항을 통해 해당 ID가 특정 프로그램(예: 특정 등급)을 나타낼 수 있으며 ID는 연결된 채널을 계속 식별합니다.

## 위험 인덱스 - 사용 {#risk-index-usage}

공유 계정에서 사용이라고도 하는 이 값은 각 계정의 공유 확률에 따라 가중치가 적용된 각 계정에서 수행한 재생 요청 수를 기반으로 계산됩니다. 공유 계정 위험 지수별 사용이라고도 합니다.

## 세그먼트 {#segmet-def}

세그먼트는 선택한 지표에서 지정한 사용자 정의 조건을 충족하는 계정 세트입니다(예: &quot;채널 X, Y 또는 Z를 시청한 MVPD A, B, C, D 또는 E 사용자&quot;).

## 공유 수준 {#sharing-level-def}

위험 인덱스 - 계정 또는 공유 계정 위험 지표라고도 하는 이 값은 선택한 기간 동안 선택된 프로그래머 채널 중 하나에서 스트리밍된 선택된 MVPD 집합에 있는 모든 계정에 대해 계산된 공유 확률을 바탕으로 계산된 값입니다.

## 정적 장치 {#static-device-def}

이동성이 매우 낮은 장치. 예를 들어, 게임 콘솔, 셋톱 박스 및 TV 세트가 있습니다.

## 시간대 {#time-frame-def}

기간 또는 시간 슬롯이라고도 하며 사용자 인터페이스에 표시되는 재생 요청 활동이 포함된 시간대이며 시작부터 끝까지 표가 표시됩니다.

## 세그먼트에서 상위 MVPD {#top-mvpds-def}

선택한 세그먼트의 상위(최대 10개) MVPD가 공유 수준, 공유 계정의 사용 또는 전체 공유 점수 중 하나의 측정값으로 설정됩니다.

## 트렌드 {#trend-def}

현재 기간과 이전 기간 간의 연결된 지표(예: 총 재생 요청 비율)의 백분율 차이입니다.

## 고유 구독자 {#unique-subscriber-def}

일정 기간 프로그래머 TV Everywhere 앱이나 Adobe Pass 관련 사이트와 상호 작용한 기간 고유 MVPD 계정 수.  이러한 상호 작용에는 Adobe Pass 서비스를 호출하는 프로그래머 앱 또는 사이트의 모든 활동이 포함됩니다. 예를 들어 authN 또는 authZ 상태를 확인하고 인증 및 인증을 수행합니다. 프로그래머가 Adobe TempPass(무료 미리 보기)를 사용하는 경우 해당 세그먼트의 고유 장치 수도 총 고유 구독자 수에 포함됩니다.

## 사용 {#usage-defs}

### Avid 사용자 {#avid-user-def}

매월 37개 이상의 재생 요청.

### 자주 사용하지 않는 사용자 {#infrequent-users-def}

월별 재생 요청이 9개 미만입니다.

### 일반 사용자 {#regular-user-def}

매월 9~37개의 재생 요청.

## 사용 패턴 {#usage-patern-def}

소셜 그룹 또는 행동(예: 소규모 가족, 여행자 또는 통근, 소셜 공유 등)에 따라 계정 사용자를 가장 잘 활용하는 계정에 적용되는 유한 카테고리 레이블 세트 중 하나입니다.

## 우편 번호 {#zip-code-def}

미국 내 위치와 연관된 미국 우편 번호.

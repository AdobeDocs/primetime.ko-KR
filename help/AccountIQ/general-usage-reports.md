---
title: 일반 사용량 보고서
description: 일반 사용량 보고서
exl-id: 1272073a-61fe-47ec-aced-2e8055b6b11e
source-git-commit: a2181a8fd7334f19b8387a31c71527d4f689ab9d
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 일반 사용량 보고서 {#general-usage-reports}

계정 IQ 보고서는 데이터를 세분화하여 분리할 수 있는 기본 분석 도구 및 보고서입니다 [집단](/help/AccountIQ/product-concepts.md#segmet-def), 예외 항목을 식별하고 계정 특성에 대한 이해를 구성합니다.

일반 사용량 보고서 페이지에서는 사용 중인 계정 장치 수, 감지된 IP 및 각 우편번호에 따라 하위 그룹 지표를 분할하는 도구를 제공합니다.

<!--Divide the content in cohorts.

Content filters
device filters

segment and definition replicate to cohorts. Number of people and number of account that ......
content consumption.....-->

보고서는 모두 [세그먼트 및 시간대](/help/AccountIQ/howto-select-segment-timeframe.md) 패널. (장치 수, IP 수 및 ZIP 코드 수) 임계값을 지정하여 선택 사항을 세밀하게 조정하고 세부적으로 세부적으로 줄일 수 있습니다 [스냅샷 개요 - 임계값을 초과하는 계정](#snapshot-overview) 패널.

<!--To view General Usage Reports:

1. Select the desired MVPDs from the **MVPDs in Segment** option.

2. Select the desired programmer channels from the **Channels in Segment** Option.

3. Select an appropriate time frame from the **Granularity and time frame** option.

   Using the above options you have defined segments for your analysis. Based on your segment selection, following graphs and reports are displayed.

4. You can fine tune your selection and further narrow it down by specifying (number of devices, number of IPs, and number of zip codes) thresholds in [Snapshot Overview - Accounts above thresholds](#snapshot-overview) widget/panel.-->

## AuthN OK / AuthZ OK / Play 요청 / 고유 구독자 {#authn-authz-playreq-uniquesubs}

여기에 있는 선 그래프는 정의된 세그먼트에 대해 선택한 기간 내에 AuthN OK, AuthZ OK, Play 요청 및 고유 구독자 값의 시간에 따른 변경 사항을 볼 수 있도록 합니다.

+++Programmer- **AuthN OK / AuthZ OK / Play 요청 / 고유 구독자**

![](assets/progr-line-graph-gu.png)


*그림: AuthN OK / AuthZ OK / Play 요청 / 프로그래머 사용자의 고유 가입자*


+++


+++MVPD- **AuthN OK / AuthZ OK / 고유 구독자**

![](assets/mvpd-line-graph-gu.png)


*그림: AuthN OK / AuthZ OK / MVPD 사용자의 고유 가입자*


+++

x축은 현재 시간 프레임 내의 단위를 나타내며 y축은 해당 기간 동안의 기본 가입자 활동 지표를 나타냅니다. 선 그래프를 사용하면 세그먼트 선택 패널에서 선택한 MVPD 구독자와 채널에 대해 다음 값을 비교할 수 있습니다.

* **AuthN 확인**

   AuthN OK는 성공한 인증 수입니다. 자세한 내용 및 정의는 다음을 참조하십시오 [제품 개념: AuthN 확인](/help/AccountIQ/product-concepts.md#authn-ok-def).

* **AuthZ 확인**

   AuthZ OK 는 성공한 권한 수입니다. 자세한 내용 및 정의는 다음을 참조하십시오 [제품 개념: AuthZ 확인](/help/AccountIQ/product-concepts.md#authz-ok-def).

* **요청 재생**

   재생 요청은 재생 요청 수입니다. 자세한 내용 및 정의는 다음을 참조하십시오 [제품 개념: 요청 재생](/help/AccountIQ/product-concepts.md#play-requests-def)

   >[!NOTE]
   >
   >MVPD 사용자는 재생 요청 선 그래프를 사용할 수 없습니다.


* **고유 구독자**

   고유 구독자는 성공한 고유 구독자의 수입니다. 자세한 내용 및 정의는 다음을 참조하십시오 [제품 개념: 고유 구독자](/help/AccountIQ/product-concepts.md#unique-subscriber-def)

   >[!NOTE]
   >
   >또한 총 고유 구독자 수에는 프로그래머가 Adobe TempPass(무료 미리 보기)를 사용하는 것이 세그먼트의 일부인 경우 고유 장치 수도 포함됩니다.

## 스냅샷 개요 - 임계값을 초과하는 계정 {#snapshot-overview}

이 추가 필터를 사용하여 분석 및 보고서를 미세 조정하여 다양한 사용 임계값을 설정합니다. 원하는 MVPD 및 채널을 선택하여 분석할 세그먼트(또는 집단)를 정의하고 나면 다음 필터를 사용하여 구독자 동작을 분석할 수도 있습니다.

* 장치 임계값 수

* IP 임계값 수

* 우편 번호 임계값 수

에서 임계값을 업데이트하는 경우 [계정 세그먼트 - 선택한 임계값 기반](#account-segments-basedon-segments) 패널에서는 다음 위치에서 영향을 볼 수 있습니다.

* [계정당 주(또는 월) 장치](#devices-week-account)

* [계정당 주(또는 월) 위치](#locations-week-account)

* [계정당 주(또는 월) IP](#ip-week-account)

* [계정 세그먼트의 내역 보기](#account-segment-historical-view)

>[!NOTE]
>
>각 임계값의 기본값은 4입니다. 즉, 일반 사용량 페이지는 4개(및 4개 이상) 이상의 장치를 사용하는 가입자를 대상으로 하여 4개 이상의 서로 다른 지리적 위치와 4개의 서로 다른 우편번호를 사용하는 MVPD에 대한 분석을 보여줍니다.

### 계정 세그먼트 - 선택한 임계값 기반 {#account-segments-basedon-segments}

다음 **계정 세그먼트 - 선택한 임계값 기반** 패널에서는 장치 수, IP 수 및 Zip 코드 수에 대한 임계값을 설정(1에서 10 사이)할 수 있는 옵션을 제공합니다.

그래프에는 다음이 표시됩니다.

* 가입자 계정의 절대 수 및

* 해당 세그먼트의 총 가입자 계정 중 백분율,

   기간 동안 X개의 장치, Y개의 IP 및 Z개의 Zip 코드를 사용하여 (정의된) MVPD에 대해 채널의 컨텐츠를 소비합니다.

![](assets/select-thresholds.png)

## 계정당 주(또는 월) 장치 {#devices-week-account}

다음 **막대 그래프** 구독자가 장치를 사용하여 콘텐츠에 액세스하는 방법과 관련된 사용 동작에 대한 통찰력을 제공합니다.

x축은 계정 수를 그래프하며 y축은 장치 수를 그래프로 표시합니다. 계정당 장치 수에 대해 설정한 임계값을 기준으로 한 주 동안 특정 장치 수의 컨텐츠를 사용하는 구독자 계정의 절대 수를 표시합니다.

![](assets/bar-gr-devices-w-acc.png)

막대(장치 수에 따라)를 마우스로 가리키면 한 주에 해당 많은 장치를 사용하여 스트리밍 채널 컨텐츠를 제공하는 가입자 계정 수(및 세그먼트에서 총 가입자 계정 중 비율)에 대한 정보를 제공하는 레이블이 나타납니다.

그래프에는 다음과 같은 표시도 있습니다.

* 설정한 임계값을 표시하는 빨간색 선입니다.

* 주(또는 월) 구독자 계정에서 사용하는 다른 장치 수의 평균을 표시하는 녹색 라인입니다.

한 계정에서 사용하는 여러 장치의 주별 평균 수와 임계값 수준을 비교하여 공유 수준을 판단할 수 있습니다.

또한 그래프는 설정된 임계값보다 더 많은 수의 장치를 사용하는 가입자 계정의 백분율을 보여줍니다.

도넛 차트는 설정된 임계값(시간대에 있음)보다 많은 장치를 사용하여 채널 컨텐츠를 사용하는 가입자 계정의 크기를 한 눈에 판별하는 데 도움이 됩니다.

![](assets/donut-devices-w-acc.png)

## 계정당 주(또는 월) 위치 {#locations-week-account}

좋아요 [계정당 주(또는 월) 장치](#devices-week-account)를 설정하는 경우, 계정당 주(또는 월) 위치 지표를 사용하면 다른 위치에서 가입자 계정 사용을 분석하여 암호 공유를 더 잘 식별할 수 있습니다. x축은 계정 수를 그래프하며 y축은 위치 수를 그래프로 표시합니다.

이 지표의 결과와 [계정당 주(또는 월) 장치](#devices-week-account) 및 번호 [계정당 주(또는 월) IP](#ip-week-account) 암호 공유 인스턴스를 보다 정확하게 판단할 수 있도록 도와줍니다. 실제 사용자는에서 계산되지 않습니다.

![](assets/graph-loc-week-acc.png)

세그먼트를 정의하고 위치 수에 대한 임계값을 설정한 후 그래프에서 를 식별할 수 있습니다.

* 1주일 동안 (특정) x 위치의 콘텐츠를 소비하는 구독자의 수(및 백분율).

* 임계값보다 많은 위치에서 콘텐츠를 보고 있는 총 가입자 계정의 비율입니다.

* 주별 평균(계정에 대해 다른 위치 수)을 임계값과 비교합니다.

## 계정당 주(또는 월) IP {#ip-week-account}

과 유사함 [계정당 주(또는 월) 장치](#devices-week-account) 및 [계정당 주(또는 월) 위치](#locations-week-account), **계정당 주당 IP 수** 지표를 사용하면 암호 공유를 보다 정확하고 세부적으로 분석할 수 있습니다.

x축은 계정 수를 그래프하며 y축은 IP 수를 그래프합니다.

![](assets/graph-ip-week-acc.png)

세그먼트를 정의하고(MVPD 및 채널을 선택하여) IP 수 임계값을 설정하면 그래프에서 다음을 식별할 수 있습니다.

* 한 주에 (특정) x 개수의 IP에서 컨텐츠를 사용하는 구독자의 수(및 백분율).

* 임계값보다 많은 IP 주소의 콘텐츠를 보고 있는 총 가입자 계정의 비율입니다.

* 주별 평균(계정에 대해 다른 IP 수)을 임계값과 비교합니다.

## 계정 세그먼트 - 내역 보기 {#account-segment-historical-view}

기록 보기 막대 그래프는 여러 다른 시간대에 있는 사용량 지표를 비교하는 데 도움이 됩니다. 또한 다음과 같은 다양한 사용 지표를 전체적으로 그래프로 표시합니다 [계정당 주(또는 월) 장치](#devices-week-account), [계정당 주(또는 월) 위치](#locations-week-account), 및 [계정당 주(또는 월) IP](#ip-week-account).

* x축은 시간 프레임을 플로팅하며 y축은 가입자 계정, 장치, 위치 및 IP의 수를 그래프로 표시합니다.

* 주황색 막대는 다양한 시간대에 있는 세그먼트를 나타냅니다.

* 선 그래프는 의 변경 사항을 표시합니다. [계정당 주(또는 월) 장치](#devices-week-account), [계정당 주(또는 월) 위치](#locations-week-account), 및 [계정당 주(또는 월) IP](#ip-week-account) 임계값을 기반으로 하여 기간 동안의 값을 표시합니다.

![](assets/historical-view.png)

* 파란색 막대는 한 기간 동안 업계에서 총 활성 구독자 수를 나타냅니다.

* 특정 범례를 선택할 수 있으며 이러한 범례가 그래프를 조정하는 데 도움이 됩니다.

![](assets/historical-view-total.png)

>[!MORELIKETHIS]
>
>* 을 사용하여 일반 사용량 보고서의 필터를 사용하여 선택한 세그먼트에서 상위 1000명의 구독자에 대한 보고서를 내보내는 방법을 알아봅니다. [상위 1000개 계정 내보내기](/help/AccountIQ/export-acc-information.md) 선택 사항입니다.


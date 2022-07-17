---
title: 계정 IQ의 작업
description: 계정 IQ의 작업에는 가입자 계정에 자동 및 대량 작업을 수행하고 그 효과를 추적하는 작업이 포함됩니다.
source-git-commit: e61cca77bad4f01de871e300dc99d7368c283f2a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# 작업 {#operations-tab-next-steps}

구독자의 사용 패턴 및 선택한 세그먼트에 대한 암호 공유를 식별한 경우(계정 IQ의 보고서 및 분석 사용), 타겟팅된 작업을 수행하여 암호 공유를 완화할 수 있습니다.

계정 IQ의 작업 기능을 사용하면 작업이라는 중요 절차를 통해 자격 증명 공유를 효과적으로 해결하고 관리할 수 있습니다. 이 옵션을 사용하면 특정 가입자 계정 그룹에 대한 객관적이고 맞춤 타깃팅된 작업(목표에 따라)을 디자인하고 향후 지속 기간 동안 실행을 자동화할 수 있습니다. 작업 기능을 통해 작업을 만들고 실행할 수 있을 뿐만 아니라 영향을 측정할 수도 있습니다. 따라서 영향을 도출하여 전략을 조정하여 채무자 또는 자격 증명 공유를 완화하든 간에 효과를 최적화할 수 있습니다.

보려면 **작업** 페이지 선택 **작업** 옵션 아래의 **작업** 계정 IQ 애플리케이션의 왼쪽 탐색에서 를 클릭합니다. 작업 페이지에는 계정 IQ 시스템에 이미 있는 모든 작업이 세부 정보와 함께 나열됩니다.

![](assets/operations-page.png)

*그림: 계정 IQ의 기존 작업 목록 및 세부 정보*

작업 페이지에서 다음을 수행할 수 있습니다.

* 계정 IQ에 이미 있는 작업 목록 보기

* 다음과 같은 작업 세부 정보를 봅니다.

   * 상태(예약됨, 실행 중, 종료됨, 오류 또는 중지됨)

   * 진행률(완료율)

   * 타겟 대상(작업을 실행할 세그먼트)

   * 스케줄(작업의 시작 및 종료 날짜)

   * 작업 생성 및 종료 날짜

* [새 작업 만들기](/help/AccountIQ/operation-affecting-user-segment.md)

* [작업 보고서 보기](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## 작업 보고서 보기 {#operation-reports}

해당 보고서를 보고 작업의 영향을 분석할 수 있습니다. 작업의 보고서를 보려면

1. 기본 작업 페이지에서 작업 이름을 선택합니다.

   보고서는 누적 막대 그래프 형태로 표시됩니다.

   ![](assets/operation-impact-report.png)

   *그림: 작업 보고서를 통해 작업의 영향을 확인할 수 있습니다*

   x축은 평가 기간을 그래프하고 y축은 작업의 영향을 측정하기 위한 변수를 그래프로 표시합니다.

   예를 들어 위의 이미지에서 y축의 변수는 계정 수입니다. 그래프를 보면 공정 세그먼트에 있는 계정 수와 특정 시간에 공정 세그먼트 외부에 있는 계정 수(예: 공정 평가 기간의 2주)를 비교할 수 있습니다. 따라서 평가 기간 동안 운영 세그먼트 내 및 세그먼트 외부에서 계정 수가 어떻게 다른지 분석할 수 있습니다.

   따라서, 작업이 의심스러운 계정에 경고 이메일을 보내는 것이었고, 작업 세그먼트의 계정이 90개 이상의 확률을 공유하고 5개 이상의 장치를 사용하여 컨텐츠를 스트리밍하는 사람들이라면, 세그먼트의 평가 기간 시작 부분에서 700만 개 이상의 계정이 발생합니다. 이 숫자는 그래프에 표시된 것처럼 평가 기간 동안 변경되므로 작업의 영향을 나타냅니다. 평가를 기반으로, 의심스러운 계정에 대해 해결하기 위한 조치를 취하거나 작업을 계속 수행하거나, 더 나은 결과를 얻기 위해 전략을 조정하여 자격 증명 공유를 억제할 수 있습니다.

2. 보고서를 닫고 기본 작업 페이지로 돌아가려면 를 선택합니다 **작업** 옵션 아래의 **작업** 왼쪽 탐색.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->
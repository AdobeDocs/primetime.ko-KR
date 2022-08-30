---
title: 계정 IQ의 작업
description: 계정 IQ의 작업에는 가입자 계정에 자동 및 대량 작업을 수행하고 그 효과를 추적하는 작업이 포함됩니다.
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 40239b6715d8eab95bc2564fb19eb6832387ad3e
workflow-type: tm+mt
source-wordcount: '467'
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

   X축은 평가 기간을 나타내고 y축은 작업의 영향을 나타냅니다(평가 기간 동안 세그먼트의 계정 수 조건). 각 막대는 세 부분으로 나뉘어져 있습니다.

   * 한 부분은 여전히 작업 세그먼트의 기준을 충족하는 계정 수를 나타냅니다.

   * 다른 부분은 원래 세그먼트에 있었지만 더 이상 작업 세그먼트의 기준을 충족하지 않는 해당 기간에 대한 활성 계정 수를 나타냅니다.

   * 세 번째 부분은 해당 기간에 활성화되지 않은 계정을 나타냅니다.
   >[!NOTE]
   >
   >첫 번째 막대는 평가 기간 시작 시 작업 세그먼트의 조건을 충족하는 계정 수를 나타냅니다.

   시간이 지나면서 그래프에는 원래 기준과 관련하여 자신의 동작을 변경한 계정 수(예: 90개 이상 및 5개 이상의 장치를 사용하는 경우)를 표시하여 작업(작업을 통해)의 효과가 표시됩니다.

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. 보고서를 닫고 기본 작업 페이지로 돌아가려면 를 선택합니다 **작업** 옵션 아래의 **작업** 왼쪽 탐색.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->
---
title: 선택 대화 상자에 MVPD가 표시되지 않도록 합니다.
description: 선택 대화 상자에 MVPD가 표시되지 않도록 합니다.
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 선택 대화 상자에 MVPD가 표시되지 않도록 합니다.

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 문제 {#issue-prevent-mvpd-sel-dialog}

MVPD 선택기에 (&quot;블록 목록&quot;) 특정 MVPD가 표시되지 않도록 해야 합니다.


## 솔루션 {#solution-prevent-mvpd-sel-dialog}

솔루션이란 `displayProviderDialog()` 가 호출됩니다.

예를 들어 CableCompany_1 및 CableCompany_2가 MVPD 선택기 내에 표시되지 않도록 하려면 다음 예에 표시된 것과 같은 작업을 수행합니다.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```

<!--
**Related Information**

* [Allow MVPDs in the Selection Dialog](/help/authentication/allow-mvpd-selectn-dialog.md)
* **Code samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->
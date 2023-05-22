---
title: 정책 업데이트 목록
description: 정책 업데이트 목록
copied-description: true
exl-id: 78078e95-775e-4c64-ab0f-d8bf644f3aee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 정책 업데이트 목록 {#policy-update-list}

정책 업데이트 목록을 사용하여 라이선스 서버에 정책 변경 사항을 전달할 수 있습니다. 정책을 콘텐츠를 패키지하는 데 사용한 후에 수정한 경우에는 라이선스 서버에서 정책의 최신 버전을 인식하도록 하여 해당 버전을 사용하여 라이선스를 발급할 수 있도록 하는 것이 좋습니다.

정책 업데이트 목록을 처음 만들려면 **[!UICONTROL Add policies]** 서버에서 사용 가능한 모든 정책을 봅니다. 콘텐츠를 패키징하는 데 사용된 후 업데이트된 정책의 경우 **[!UICONTROL update]** 라디오 단추.

더 이상 정책을 사용하여 라이선스를 발급하지 않으려는 경우 해당 정책이 이미 콘텐츠를 패키지화하는 데 사용되었다면 정책을 취소할 수 있습니다. 이렇게 하려면 **[!UICONTROL revoke]** 라디오 단추. 원하는 정책을 선택한 경우 다음을 선택합니다 **[!UICONTROL Create Policy Update List]**. 라는 파일 [!DNL PolicyUpdateList.dat] 이(가)에 저장됩니다. [!DNL Resources] 디렉토리.

기존 정책 업데이트 목록을 수정하려면 **[!UICONTROL Add policies]** 서버에서 사용 가능한 모든 정책을 봅니다. 추가하거나 취소할 추가 정책을 선택합니다. 정책 업데이트 목록의 기존 항목은 화면의 상단 섹션에서 변경할 수 있습니다. 표시된 정책 **[!UICONTROL updated]** 다음으로 변경될 수 있음: **[!UICONTROL revoked]**, 그러나 정책이 다음과 같은 경우: **[!UICONTROL revoked]**&#x200B;로 다시 변경할 수 없습니다. **[!UICONTROL updated]**.

원하는 변경이 이루어지면 다음을 선택합니다 **[!UICONTROL Create Policy Update List]**&#x200B;및 [!DNL PolicyUpdateList.dat] 파일이 다시 생성됩니다. 정책이 이미 정책 업데이트 목록에 있고, 목록이 마지막으로 생성된 이후에 업데이트된 경우 정책 업데이트 목록이 다시 생성될 때 정책의 최신 버전이 사용됩니다.

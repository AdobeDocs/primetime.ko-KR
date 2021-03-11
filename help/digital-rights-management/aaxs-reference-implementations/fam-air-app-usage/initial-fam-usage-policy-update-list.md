---
title: 정책 업데이트 목록
description: 정책 업데이트 목록
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# 정책 업데이트 목록 {#policy-update-list}

정책 업데이트 목록을 사용하여 라이센스 서버에 정책 변경 사항을 알릴 수 있습니다. 정책을 컨텐츠 패키징에 사용한 후 수정할 경우 라이센스 서버에 최신 버전의 정책을 인식하여 해당 버전을 라이센스 발급에 사용할 수 있도록 하는 것이 좋습니다.

처음으로 정책 업데이트 목록을 만들려면 **[!UICONTROL Add policies]**&#x200B;을 클릭하여 서버에서 사용 가능한 모든 정책을 봅니다. 컨텐츠를 패키지하는 데 사용한 이후 업데이트된 모든 정책의 경우 **[!UICONTROL update]** 라디오 단추를 선택합니다.

더 이상 정책을 사용하여 라이선스를 발급하지 않으려는 경우 해당 정책이 콘텐츠를 패키지하는 데 이미 사용된 경우 해당 정책을 취소할 수 있습니다. 이렇게 하려면 **[!UICONTROL revoke]** 라디오 단추를 선택합니다. 원하는 정책을 선택한 경우 **[!UICONTROL Create Policy Update List]**&#x200B;을 선택합니다. [!DNL PolicyUpdateList.dat]이라는 파일이 [!DNL Resources] 디렉토리에 저장됩니다.

기존 정책 업데이트 목록을 수정하려면 **[!UICONTROL Add policies]**&#x200B;을 클릭하여 서버에서 사용 가능한 모든 정책을 봅니다. 추가하거나 취소할 추가 정책을 선택합니다. 정책 업데이트 목록의 기존 항목은 화면의 위쪽 섹션에서 변경할 수 있습니다. **[!UICONTROL updated]**&#x200B;으로 표시된 정책은 **[!UICONTROL revoked]**&#x200B;로 변경할 수 있지만, 정책이 **[!UICONTROL revoked]**&#x200B;이면 **[!UICONTROL updated]**&#x200B;으로 다시 변경할 수 없습니다.

원하는 변경 사항이 적용되면 **[!UICONTROL Create Policy Update List]**&#x200B;을 선택하고 [!DNL PolicyUpdateList.dat] 파일이 다시 생성됩니다. 정책이 이미 정책 업데이트 목록에 있고 마지막으로 목록을 생성할 때부터 업데이트된 경우 정책 업데이트 목록이 다시 생성되면 정책의 최신 버전이 사용됩니다.

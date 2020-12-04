---
seo-title: 정책 업데이트 목록
title: 정책 업데이트 목록
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# 정책 업데이트 목록 {#policy-update-list}

정책 업데이트 목록을 사용하여 라이센스 서버에 정책 변경 사항을 알릴 수 있습니다. 정책을 컨텐츠 패키징하는 데 사용한 후 수정할 경우 라이센스 서버에 최신 버전의 정책을 인식하여 버전을 라이센스 발급에 사용하는 것이 좋습니다.

처음으로 정책 업데이트 목록을 만들려면 **[!UICONTROL Add policies]**&#x200B;을 클릭하여 서버에서 사용 가능한 모든 정책을 봅니다. 컨텐츠를 패키지하는 데 사용한 이후 업데이트된 모든 정책의 경우 **[!UICONTROL update]** 라디오 단추를 선택합니다.

더 이상 정책을 사용하여 라이선스를 발급하지 않으려는 경우 해당 정책이 이미 콘텐츠를 패키지하는 데 사용되었다면 정책을 취소할 수 있습니다. 이렇게 하려면 **[!UICONTROL revoke]** 라디오 단추를 선택합니다. 원하는 정책을 선택한 경우 **[!UICONTROL Create Policy Update List]**&#x200B;을 선택합니다. [!DNL PolicyUpdateList.dat]이라는 파일이 [!DNL Resources] 디렉토리에 저장됩니다.

기존 정책 업데이트 목록을 수정하려면 **[!UICONTROL Add policies]**&#x200B;을 클릭하여 서버에서 사용 가능한 모든 정책을 봅니다. 추가하거나 취소할 추가 정책을 선택합니다. 정책 업데이트 목록의 기존 항목은 화면의 상단 섹션에서 변경할 수 있습니다. **[!UICONTROL updated]**&#x200B;으로 표시된 정책은 **[!UICONTROL revoked]**&#x200B;로 변경할 수 있지만, 정책이 **[!UICONTROL revoked]**&#x200B;이면 **[!UICONTROL updated]**&#x200B;으로 다시 변경할 수 없습니다.

원하는 변경 사항이 적용되면 **[!UICONTROL Create Policy Update List]**&#x200B;을 선택하면 [!DNL PolicyUpdateList.dat] 파일이 다시 생성됩니다. 정책이 정책 업데이트 목록에 이미 있고 마지막으로 목록을 생성한 이후로 업데이트된 경우 정책 업데이트 목록이 다시 생성될 때 최신 버전의 정책이 사용됩니다.

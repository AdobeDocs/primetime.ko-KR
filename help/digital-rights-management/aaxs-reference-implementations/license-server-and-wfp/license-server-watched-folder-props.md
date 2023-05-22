---
title: 감시 폴더 속성
description: 감시 폴더 속성
copied-description: true
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 감시 폴더 속성 {#watched-folder-properties}

각 감시 폴더에는 라는 파일이 있습니다. [!DNL properties/watchfolder.properties]. 이 파일에는 암호화할 내용 및 적용할 정책을 포함하여 이 폴더에 배치된 콘텐츠의 패키징 옵션이 포함되어 있습니다. 속성 파일의 값에 대한 모든 변경 사항은 다음에 감시 폴더 패키저가 실행될 때 적용됩니다(서버를 다시 시작할 필요가 없음).

packager 속성 파일에 구성 오류가 있으면 packager 스레드가 중지됩니다. 감시 폴더 패키지를 다시 시작하려면 서버를 다시 시작합니다. 감시 폴더 속성 파일에 구성 오류가 있는 경우 감시 폴더는 패키저가 처리하는 폴더 목록에서 일시적으로 제거됩니다. 감시 폴더를 목록에 다시 추가하려면 서버를 다시 시작하거나 패키지 속성 파일을 수정하십시오. 특정 파일을 패키지하는 동안 오류가 발생하면(예: 파일이 손상되었기 때문에) 파일을 건너뛰고 폴더의 나머지 파일을 처리합니다.

---
seo-title: 감시 폴더 속성
title: 감시 폴더 속성
uuid: fc204bb4-033a-46fe-8642-737f6a4cd1f1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 감시 폴더 속성 {#watched-folder-properties}

시청 중인 각 폴더에는 [!DNL properties/watchfolder.properties]이라는 파일이 포함되어 있습니다. 이 파일에는 암호화할 항목 및 적용할 정책을 비롯하여 이 폴더에 저장된 컨텐츠에 대한 패키징 옵션이 포함되어 있습니다. 속성 파일의 값에 대한 모든 변경 사항은 다음 번에 감시 폴더 패키저가 실행될 때 적용됩니다(서버를 다시 시작할 필요가 없음).

패키지 속성 파일에 구성 오류가 있으면 패키지 스레드가 중지됩니다. 감시 폴더 패키지를 다시 시작하려면 서버를 다시 시작하십시오. 감시 폴더 속성 파일에 구성 오류가 있으면 Packager가 처리하는 폴더 목록에서 감시 폴더가 일시적으로 제거됩니다. 감시 폴더를 목록에 다시 추가하려면 서버를 다시 시작하거나 패키지 속성 파일을 수정합니다. 특정 파일을 패키지하는 동안 오류가 발생하면(예: 파일이 손상되었기 때문에) 파일을 건너뛰고 폴더의 나머지 파일이 처리됩니다.

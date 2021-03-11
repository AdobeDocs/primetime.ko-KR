---
title: Packager 속성 파일
description: Packager 속성 파일
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 패키지 속성 파일 {#packager-properties-file}

[!DNL flashaccess-refimpl-packager.properties] 파일을 사용하여 참조 구현의 감시 폴더 패키지 구성 요소를 구성합니다. 최소한 라이센스 서버 URL, 라이센스 서버 인증서, 패키지 자격 증명 및 키 보호 옵션을 설정해야 합니다. 이 파일에는 각 감시 폴더(packager.watchfolder.source)의 위치도 포함되어 있습니다. `n`). 이 속성 파일의 값에 대한 모든 변경 사항은 다음 번에 감시 폴더 패키지를 실행할 때 적용됩니다(서버를 다시 시작할 필요는 없음). 그러나 패키저에 구성 오류가 있는 경우 감시 폴더 패키지 스레드가 종료되고, 패키지 스레드를 다시 시작하려면 서버를 다시 시작해야 합니다.

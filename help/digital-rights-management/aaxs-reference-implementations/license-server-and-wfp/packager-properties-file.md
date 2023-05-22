---
title: Packager 속성 파일
description: Packager 속성 파일
copied-description: true
exl-id: 7d78576b-fd77-460d-92d9-c2e69e37006e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Packager 속성 파일 {#packager-properties-file}

사용 [!DNL flashaccess-refimpl-packager.properties] 참조 구현의 감시 폴더 패키지 구성 요소를 구성하는 파일입니다. 최소한 라이선스 서버 URL, 라이선스 서버 인증서, 패키지 자격 증명 및 키 보호 옵션을 설정해야 합니다. 이 파일에는 각 감시 폴더(packager.watchfolder.source)의 위치도 포함되어 있습니다. `n`). 이 속성 파일의 값에 대한 모든 변경 사항은 다음에 감시 폴더 패키저가 실행될 때 적용됩니다(서버를 다시 시작할 필요가 없음). 그러나 packager에 구성 오류가 있으면 감시 폴더 packager 스레드가 종료되고 packager 스레드를 다시 시작하려면 서버를 다시 시작해야 합니다.

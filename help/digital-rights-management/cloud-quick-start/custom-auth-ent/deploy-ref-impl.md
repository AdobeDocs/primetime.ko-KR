---
title: BEES 참조 구현 배포
description: BEES 참조 구현 배포
copied-description: true
exl-id: 87f3f879-66b4-4b8c-a0c4-e15551f9b727
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# BEES 참조 구현 배포 {#deploy-the-bees-reference-implementation}

1. Tomcat 애플리케이션 서버를 설정합니다. Tomcat 설명서를 참조하십시오.
1. 다음을 복사합니다. `[!DNL bees.war]` 파일을 Tomcat의 [!DNL webapps/] 폴더를 삭제합니다.
1. 다음으로 요청 보내기 `https://localhost:8080/bees`.

   &quot;BEES가 작동 중입니다.&quot;라는 메시지가 표시되면 배포가 성공적으로 완료된 것입니다.
1. 서버에서 SSL을 활성화합니다.

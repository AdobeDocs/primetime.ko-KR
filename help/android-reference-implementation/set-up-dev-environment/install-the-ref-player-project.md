---
description: TVSDK Primetime Reference는 TVSDK 및 AVE 프레임워크를 기반으로 구축된 Android 애플리케이션입니다.
title: Primetime 참조 구현 구축
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---


# Primetime 참조 구현 {#build-the-primetime-reference-implementation} 구축

TVSDK Primetime Reference는 TVSDK 및 AVE 프레임워크를 기반으로 구축된 Android 애플리케이션입니다.

Eclipse에서 Primetime 참조 프로젝트를 설정하고 빌드하려면 다음을 수행하십시오.

1. TVSDK Android zip 파일을 다운로드하여 기억할만한 위치에 있는 디렉토리에 압축 해제합니다.
1. Eclipse를 실행합니다.
1. **[!UICONTROL File]** > **[!UICONTROL Import]**&#x200B;을 선택합니다.
1. **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**&#x200B;을 선택합니다.
1. 클릭 **[!UICONTROL Next]**.
1. **[!UICONTROL Browse]** 단추를 사용하여 TVSDK Android zip 파일의 압축을 해제할 [!DNL samples/PrimetimeReference/src] 아래의 디렉토리로 **[!UICONTROL Root Directory]** 필드를 채웁니다.
1. 가져올 다음 프로젝트를 선택합니다.**[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. 클릭 **[!UICONTROL Finish]**.
1. 프로젝트를 빌드하려면 **[!UICONTROL Project]** > **[!UICONTROL Build Project]**&#x200B;을 선택합니다.

   프로젝트가 자동으로 빌드되도록 설정된 경우에는 이 단계가 필요하지 않습니다.
1. 테스트 프로젝트를 작업 공간에 포함하려면 테스트 프로젝트를 PrimetimeReference 프로젝트에 연결합니다.
   1. 3단계를 반복합니다. 6.
   1. 가져올 다음 프로젝트를 선택합니다.`PrimetimeReference\tests`.
   1. 클릭 **[!UICONTROL Finish]**.

      테스트 프로젝트는 CatalogActivity 프로젝트에 종속되므로 테스트 프로젝트를 CatalogActivity 프로젝트에 연결해야 합니다.
   1. **[!UICONTROL tests]**&#x200B;을(를) 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL Properties]**&#x200B;을 선택합니다.
   1. Java 빌드 경로 아래의 **[!UICONTROL Projects]** 탭을 선택합니다.
   1. 클릭 **[!UICONTROL Add...]**
   1. 카탈로그 활동을 선택합니다.
   1. **[!UICONTROL OK]**&#x200B;을 클릭하여 프로젝트를 추가합니다.
   1. **[!UICONTROL OK]**&#x200B;을 클릭하여 속성 페이지를 종료합니다.
   1. 프로젝트를 빌드하려면 **[!UICONTROL Project]** > **[!UICONTROL Build Project]**&#x200B;을 선택합니다.

      프로젝트가 자동으로 빌드되도록 설정된 경우에는 이 단계가 필요하지 않습니다.

---
description: TVSDK Primetime Reference는 TVSDK 및 AVE 프레임워크를 기반으로 구축된 Android 애플리케이션입니다.
seo-description: TVSDK Primetime Reference는 TVSDK 및 AVE 프레임워크를 기반으로 구축된 Android 애플리케이션입니다.
seo-title: Primetime 참조 구현 구축
title: Primetime 참조 구현 구축
uuid: ab12660a-1563-49a4-82d9-1ab13f8a92be
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Primetime 참조 구현 구축 {#build-the-primetime-reference-implementation}

TVSDK Primetime Reference는 TVSDK 및 AVE 프레임워크를 기반으로 구축된 Android 애플리케이션입니다.

Eclipse에서 Primetime Reference 프로젝트를 설정하고 빌드하려면:

1. TVSDK Android zip 파일을 다운로드하고 저장할 위치에 있는 디렉토리에 압축을 해제합니다.
1. Eclipse를 실행합니다.
1. > **[!UICONTROL File]** 를 **[!UICONTROL Import]**&#x200B;선택합니다.
1. > **[!UICONTROL Android]** 를 **[!UICONTROL Existing Android Code Into Workspace]**&#x200B;선택합니다.
1. 클릭 **[!UICONTROL Next]**.
1. 이 **[!UICONTROL Browse]** 단추를 사용하여 TVSDK Android zip 파일의 압축을 푼 **[!UICONTROL Root Directory]** [!DNL samples/PrimetimeReference/src] 디렉토리로 필드를 채웁니다.
1. 가져올 다음 프로젝트를 선택합니다. **[!UICONTROL appcompat]**&#x200B;예 **[!UICONTROL PrimetimeReference]**.
1. 클릭 **[!UICONTROL Finish]**.
1. > **[!UICONTROL Project]** 를 선택하여 **[!UICONTROL Build Project]** 프로젝트를 빌드합니다.

   프로젝트가 자동으로 빌드되도록 설정된 경우에는 이 단계가 필요하지 않습니다.
1. 테스트 프로젝트를 작업 영역에 포함하려면 테스트 프로젝트를 PrimetimeReference 프로젝트와 연결하십시오.
   1. 3단계를 반복합니다. 6.
   1. 가져올 다음 프로젝트를 선택합니다. `PrimetimeReference\tests`Adobe
   1. 클릭 **[!UICONTROL Finish]**.

      테스트 프로젝트는 CatalogActivity 프로젝트에 종속되므로 테스트 프로젝트를 CatalogActivity 프로젝트에 연결해야 합니다.
   1. 마우스 오른쪽 버튼을 클릭하고 **[!UICONTROL tests]** 선택합니다 **[!UICONTROL Properties]**.
   1. Java 빌드 경로 아래의 **[!UICONTROL Projects]** 탭을 선택합니다.
   1. 클릭 **[!UICONTROL Add...]**
   1. 카탈로그 활동을 선택합니다.
   1. 을 **[!UICONTROL OK]** 클릭하여 프로젝트를 추가합니다.
   1. 을 **[!UICONTROL OK]** 클릭하여 속성 페이지를 종료합니다.
   1. > **[!UICONTROL Project]** 를 선택하여 **[!UICONTROL Build Project]** 프로젝트를 빌드합니다.

      프로젝트가 자동으로 빌드되도록 설정된 경우에는 이 단계가 필요하지 않습니다.

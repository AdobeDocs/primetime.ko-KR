---
description: TVSDK Primetime 참조는 TVSDK 및 AVE 프레임워크를 기반으로 구축된 Android 애플리케이션입니다.
title: Primetime 참조 구현 빌드
exl-id: d2950f2b-06d7-4fc8-a031-5f058ce47545
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Primetime 참조 구현 빌드 {#build-the-primetime-reference-implementation}

TVSDK Primetime 참조는 TVSDK 및 AVE 프레임워크를 기반으로 구축된 Android 애플리케이션입니다.

Eclipse에서 Primetime 참조 프로젝트를 설정하고 빌드하려면 다음을 수행하십시오.

1. TVSDK Android zip 파일을 다운로드하고 기억할 위치의 디렉토리에 압축을 풉니다.
1. Eclipse를 시작합니다.
1. 선택 **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. 선택 **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. 클릭 **[!UICONTROL Next]**.
1. 사용 **[!UICONTROL Browse]** 버튼을 눌러 **[!UICONTROL Root Directory]** 아래에 디렉터리가 있는 필드 [!DNL samples/PrimetimeReference/src] 에 대해 TVSDK Android zip 파일의 압축을 풉니다.
1. 가져올 다음 프로젝트를 선택하십시오. **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. 클릭 **[!UICONTROL Finish]**.
1. 선택  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 프로젝트를 빌드합니다.

   프로젝트가 자동으로 빌드되도록 설정된 경우에는 이 단계가 필요하지 않습니다.
1. 작업 영역에 테스트 프로젝트를 포함하려면 테스트 프로젝트를 PrimetimeReference 프로젝트와 연결합니다.
   1. 3단계를 반복합니다. 6~6.
   1. 가져올 다음 프로젝트를 선택하십시오. `PrimetimeReference\tests`.
   1. 클릭 **[!UICONTROL Finish]**.

      테스트 프로젝트는 CatalogActivity 프로젝트에 종속되어 있으므로 테스트 프로젝트를 CatalogActivity 프로젝트와 연결해야 합니다.
   1. 마우스 오른쪽 버튼 클릭 **[!UICONTROL tests]** 및 선택 **[!UICONTROL Properties]**.
   1. 다음 항목 선택 **[!UICONTROL Projects]** Java 빌드 경로 아래의 탭입니다.
   1. 클릭 **[!UICONTROL Add...]**
   1. CatalogActivity 를 선택합니다.
   1. 클릭 **[!UICONTROL OK]** 프로젝트를 추가합니다.
   1. 클릭 **[!UICONTROL OK]** 속성 페이지를 종료합니다.
   1. 선택  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 프로젝트를 빌드합니다.

      프로젝트가 자동으로 빌드되도록 설정된 경우에는 이 단계가 필요하지 않습니다.

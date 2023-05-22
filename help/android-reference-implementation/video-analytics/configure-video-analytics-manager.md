---
description: Adobe Analytics 계정에서 작동하도록 구성하여 Primetime Android 참조 구현에서 비디오 사용을 추적할 수 있습니다.
title: 비디오 분석 구성
exl-id: 42498e2a-9ff2-442c-8cf9-bd7901f618f4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 비디오 분석 구성 {#configure-video-analytics}

Adobe Analytics 계정에서 작동하도록 구성하여 Primetime Android 참조 구현에서 비디오 사용을 추적할 수 있습니다. Android 참조 구현은 비디오 사용 및 하트비트 데이터를 Adobe Analytics으로 보내도록 설계되었습니다. 이 기능을 활성화하려면 먼저 Adobe Primetime 담당자에게 연락하여 Adobe Analytics 계정을 만들어야 합니다.

참조 구현 내에는 Adobe Analytics 통합을 활성화하기 위해 구성해야 하는 두 가지 위치가 있습니다. 런타임 비디오 분석 구성은 새 비디오를 재생하도록 선택하면(즉, 새 PlayerActivity가 생성되면) 영향을 받습니다.

1. 에서 로드 시간 옵션 구성 `ADBMobileConfig.json` 에셋 파일.

   이 파일은 Adobe 담당자가 제공합니다. 기본적으로 Primetime SDK 번들에는 포함되어 있지 않습니다. 이 구성 파일의 설정에 대한 자세한 내용은 비디오 분석 초기화 및 구성 페이지에서 Android 프로그래머 안내서를 참조하십시오.
1. 참조 구현 설정 메뉴에서 런타임 옵션 구성

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | 런타임 옵션 | 설명 |
   |---|---|
   | Video Analytics 추적 서버 | 비디오 분석 백엔드 컬렉션 끝점의 URL. 여기서 모든 비디오 하트비트 추적 호출이 전송됩니다. |
   | 작업 ID | 처리 작업 식별자. 이는 비디오 추적 호출에 적용할 처리 종류를 백엔드 끝점에 나타냅니다. |
   | 채널 | 사용자가 콘텐츠를 보고 있는 채널의 이름입니다. 모바일 애플리케이션의 경우 일반적으로 애플리케이션의 이름입니다. |
   | 게시자 | 콘텐츠 게시자의 이름 |
   | 디버그 로깅 | 광범위한 로깅을 활성화합니다. 기본적으로 비활성화되어 있으므로 활성화 시 성능에 영향을 줄 수 있으므로 프로덕션 환경에 대해 비활성화하십시오. |
   | 자동 모드 | 이 옵션을 활성화하면 네트워크 호출이 수행되지 않으므로 로컬 디버깅에 유용하지만 프로덕션 환경에서는 비활성화해야 합니다. |

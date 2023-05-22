---
description: 참조 구현 프레임워크를 기반으로 사용자 지정 사용자 인터페이스를 쉽게 빌드할 수 있습니다.
title: 사용자 지정 사용자 인터페이스 빌드
exl-id: 96008010-cd63-4fb1-a3fc-2fc94b624413
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 사용자 지정 사용자 인터페이스 빌드 {#build-a-custom-user-interface}

참조 구현 프레임워크를 기반으로 사용자 지정 사용자 인터페이스를 빌드할 수 있습니다.

다음 기능의 UI 구성 요소가 이미 통합되었습니다.

* 클릭 가능한 광고
* 광고 오버레이
* 지연 바인딩 오디오
* 폐쇄 캡션
* 위의 모든 구성 요소에 대한 리스너

1. 편집 [!DNL PlayerFragment.java] 플레이어에서 사용할 UI 구성 요소를 초기화하는 파일입니다.

1. 편집 [!DNL res/player/player_fragment.xml] 사용자 인터페이스를 사용자 지정하는 파일입니다.
1. 프로젝트를 빌드합니다.

>[!NOTE]
>
>검색 막대에 UI를 변경하기 위해 MarkableSeekBar 클래스를 편집할 수 있습니다. 다음 [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) 클래스는 슬라이더, 슬라이더의 썸네일, 광고 마커 홀더, 큐 마커, 버퍼 범위 및 검색 범위 배경을 처리합니다.

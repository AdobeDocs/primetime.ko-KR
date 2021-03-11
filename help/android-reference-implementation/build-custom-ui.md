---
description: 참조 구현 프레임워크를 기반으로 사용자 지정 사용자 인터페이스를 쉽게 만들 수 있습니다.
title: 사용자 정의 유저 인터페이스 구축
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 사용자 지정 사용자 인터페이스 {#build-a-custom-user-interface} 만들기

참조 구현 프레임워크를 기반으로 사용자 지정 사용자 인터페이스를 만들 수 있습니다.

다음 기능의 UI 구성 요소는 이미 통합되어 있습니다.

* 클릭 가능한 광고
* 광고 오버레이
* 지연 바인딩 오디오
* 자막
* 위의 모든 구성 요소에 대한 리스너

1. [!DNL PlayerFragment.java] 파일을 편집하여 플레이어에서 사용할 UI 구성 요소를 초기화합니다.

1. [!DNL res/player/player_fragment.xml] 파일을 편집하여 사용자 인터페이스를 사용자 정의합니다.
1. 프로젝트를 빌드합니다.

>[!NOTE]
>
>검색 막대를 UI로 변경하려면 MarkableSeekBar 클래스를 편집할 수 있습니다. [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) 클래스는 슬라이더, 슬라이더의 축소판, 광고 마커 홀더, 큐 마커, 버퍼 범위 및 검색 범위 배경을 처리합니다.
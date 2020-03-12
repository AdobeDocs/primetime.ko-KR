---
description: 참조 구현 프레임워크를 기반으로 사용자 지정 사용자 인터페이스를 쉽게 만들 수 있습니다.
seo-description: 참조 구현 프레임워크를 기반으로 사용자 지정 사용자 인터페이스를 쉽게 만들 수 있습니다.
seo-title: 사용자 정의 유저 인터페이스 구축
title: 사용자 정의 유저 인터페이스 구축
uuid: b785f6a4-3ef8-4f7a-a087-0d6551da9750
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 사용자 정의 유저 인터페이스 구축 {#build-a-custom-user-interface}

참조 구현 프레임워크를 기반으로 사용자 지정 사용자 인터페이스를 만들 수 있습니다.

다음 기능의 UI 구성 요소는 이미 통합되어 있습니다.

* 클릭 가능한 광고
* 광고 오버레이
* 지연 바인딩 오디오
* 자막
* 위의 모든 구성 요소에 대한 리스너

1. 플레이어에서 사용할 UI 구성 요소를 초기화하려면 [!DNL PlayerFragment.java] 파일을 편집합니다.

1. 사용자 인터페이스를 사용자 정의하려면 [!DNL res/player/player_fragment.xml] 파일을 편집합니다.
1. 프로젝트를 빌드합니다.

>[!NOTE]
>
>검색 표시줄의 UI를 변경하려면 MarkableSeekBar 클래스를 편집할 수 있습니다. Marketing [SeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) 클래스는 슬라이더, 슬라이더의 축소판, 광고 마커 홀더, 큐 마커, 버퍼 범위 및 검색 범위 배경을 처리합니다.
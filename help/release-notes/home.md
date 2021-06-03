---
title: Primetime 릴리스 정보
description: Primetime 릴리스 정보
copied-description: true
exl-id: 29087a3e-f16e-4510-8d3a-ed2229700899
source-git-commit: fe0f5f3399d2e2ab3e07713fbcd29ede47888d98
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 28%

---

# Primetime 릴리스 정보

Adobe Primetime 릴리스 노트를 시작합니다. 왼쪽 탐색에 나열된 문서는 릴리스 관련 정보, 시스템 요구 사항, 제한 사항, 해결된 문제 및 알려진 문제를 제공합니다.

## PTAI 21.5.1의 개선 사항 및 수정 사항

이 릴리스에는 예정된 대시보드 변경에 대한 새로운 원격 분석과 SCTE 기반 큐 형식에 대한 더 이상 사용되지 않는 세그먼테이션 유형 0x01(UPID)을 지원합니다.

기타 수정 사항 및 세부 사항은 [Ad Insertion 릴리스 노트](/help/release-notes/ptai-21x-release-notes.md)를 참조하십시오

## TVSDK 3.13 iOS의 개선 사항 및 수정 사항

이 릴리스에서는 LIVE, VOD 및 FER 스트림에 대한 DEMUXED &#39;HLS/CMAF&#39;(프리롤, 미드롤 및 포스트롤) 광고를 지원합니다.

기타 수정 사항 및 세부 정보는 [iOS용 TVSDK 릴리스 노트](../release-notes/tvsdk-3x-ios.md) 를 참조하십시오

## TVSDK 3.13 Android의 수정 사항

이번 릴리스는 FireTV 3세대 Pendant와 Fire TV Cube 1세대 및 2세대 장치를 포함하는 FireTV 장치의 ABR 스위치에서 Widevine DRM 스트림을 동결하거나 블랙 프레임을 표시하는 문제에 대한 해결 방법을 제공합니다.

이 문제를 해결하려면 재생을 시작하기 전에 지정된 Fire TV 장치에 대해 API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` 를 설정합니다. 기본값은 false입니다.

자세한 내용은 [Android용 TVSDK 릴리스 노트](../release-notes/tvsdk-3x-android.md)를 참조하십시오.

## 참조 -

| 사용 안내서 | 설명 |
|--- |--- |
| [Primetime 프로그래밍 도움말](/help/programming/home.md) | Android 디바이스에서 Java를 사용하는 애플리케이션 및 비디오 플레이어를 개발하는 방법과 iOS 디바이스에서 Objective-C를 사용하는 방법을 배울 수 있습니다. |
| [Primetime 마이그레이션 및 전환 도움말](/help/migration-guides/home.md) | 기존 Primetime TVSDK Suite에서 차세대 제품으로 전환하는 전환 및 마이그레이션 프로세스에 대해 설명합니다. |
| [참조 구현](/help/android-reference-implementation/home.md) | TVSDK를 이해하고 기능 관리자를 수정하여 개인 플레이어를 사용자 정의할 수 있습니다. |
| [Primetime API 참조](/help/reference/api-references.md) | TVSDK 함수, 데이터 구조 및 기타 프로그래밍 구문에 대한 자세한 정보를 제공합니다. |
| [Digital Rights Management](/help/digital-rights-management/home.md) | Digital Rights Management(DRM)의 다양한 사용자 시나리오에 대해 자세히 알아보십시오 |
| [Primetime Ad Insertion 도움말](/help/primetime-ad-insertion/home.md) | 서버에 사용자 타겟팅된 동적 광고를 삽입하여 컨텐츠를 상용화하고 개인화된 광고를 통해 고객의 참여를 유도하는 방법을 설명합니다. |
| [아카이브](https://helpx.adobe.com/primetime/archives.html) | 보관된 설명서의 PDF를 다운로드합니다. |

## 유용한 리소스

* [Adobe Primetime 알기](https://www.adobe.com/in/marketing/primetime.html)

* [동시성 모니터링](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Primetime 인증](https://tve.helpdocsonline.com/home)

* [Adobe Primetime DRM 포럼](https://forums.adobe.com/community/adobe_access)

* [Adobe Primetime 개발자 리소스](https://www.adobe.com/devnet/primetime.html)

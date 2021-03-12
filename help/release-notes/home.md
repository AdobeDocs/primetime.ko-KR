---
title: Primetime 릴리스 노트
description: Primetime 릴리스 노트
copied-description: true
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 26%

---


# Primetime 릴리스 노트

Adobe Primetime 릴리스 노트입니다. 왼쪽 탐색에 나열된 문서는 릴리스별 정보, 시스템 요구 사항, 제한 사항, 해결된 문제 및 알려진 문제를 제공합니다.

## TVSDK 3.13 iOS의 향상된 기능 및 수정 사항

이번 릴리스에서는 LIVE, VOD 및 FER 스트림에 대한 DEMUXED &#39;HLS/CMAF&#39;(프리롤, 미드롤 및 포스트롤) 광고 지원이 도입되었습니다.

기타 수정 사항과 자세한 내용은 [iOS용 TVSDK 릴리스 노트](../release-notes/tvsdk-3x-ios.md)를 참조하십시오.

## PTAI 21.2.2 개선 사항 및 수정 사항

이번 릴리스에서는 HLS 스트림에서 EXT-X-IMAGE-STREAM-INF 스트림 삽입/동기화를 지원합니다. 이 기능은 서버측 구성을 통해 활성화됩니다. 이 기능을 활성화하려면 기술 계정 담당자에게 문의하십시오.

## TVSDK 3.13 Android의 수정 사항

이 릴리스에서는 Fire TV 3세대 Pendant 및 Fire TV Cube 1세대 및 2세대 장치를 포함하는 FireTV 장치의 ABR 스위치에 검정 프레임이 표시되거나 Widevine DRM 스트림에 대한 문제를 해결합니다.

이 문제를 해결하려면 재생을 시작하기 전에 지정된 Fire TV 장치에 대한 API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)`를 설정하십시오. 기본값은 false입니다.

자세한 내용은 [TVSDK for Android 릴리스 노트](../release-notes/tvsdk-3x-android.md)를 참조하십시오.

## TVSDK 3.12 iOS 릴리스 노트의 개선 사항 및 수정 사항

이 릴리스는 주요 고객 문제 해결에 중점을 두었습니다.

[iOS](../release-notes/tvsdk-3x-ios.md)에 대해 현재 릴리스된 버전에 대한 자세한 내용을 확인하십시오.

## 참조 항목

| 사용 안내서 | 설명 |
|--- |--- |
| [Primetime 프로그래밍 도움말](/help/programming/home.md) | Android 장치에서 Java를 사용하는 응용 프로그램 및 비디오 플레이어를 개발하는 방법과 iOS 장치에서 Objective-C를 사용하는 방법을 배울 수 있습니다. |
| [Primetime 마이그레이션 및 전환 도움말](/help/migration-guides/home.md) | 기존 Primetime TVSDK Suite에서 차세대 제품으로 전환하는 전환 및 마이그레이션 프로세스에 대해 설명합니다. |
| [참조 구현](/help/android-reference-implementation/home.md) | TVSDK를 이해하고 기능 관리자를 수정하여 개인 플레이어를 사용자 정의할 수 있습니다. |
| [Primetime API 참조](/help/reference/api-references.md) | TVSDK 함수, 데이터 구조 및 기타 프로그래밍 구문에 대한 자세한 정보를 제공합니다. |
| [Digital Rights Management](/help/digital-rights-management/home.md) | Digital Rights Management(DRM)의 다양한 사용자 시나리오에 대해 자세히 알아보려면 도움이 됩니다. |
| [Primetime Ad Insertion 도움말](/help/primetime-ad-insertion/home.md) | 서버에 사용자 타겟팅된 동적 광고를 삽입하여 컨텐츠를 상용화하고 개인화된 광고를 통해 고객의 참여를 유도하는 방법을 설명합니다. |
| [아카이브](https://helpx.adobe.com/primetime/archives.html) | 보관된 문서의 PDF를 다운로드합니다. |

## 유용한 리소스

* [Adobe Primetime 개요](https://www.adobe.com/in/marketing/primetime.html)

* [동시 시청 모니터링](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Primetime 인증](https://tve.helpdocsonline.com/home)

* [Adobe Primetime DRM 포럼](https://forums.adobe.com/community/adobe_access)

* [Adobe Primetime 개발자 리소스](https://www.adobe.com/devnet/primetime.html)

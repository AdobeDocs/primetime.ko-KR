---
description: 이 안내서에서는 브라우저 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.
title: 제품 개요 및 대상
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 제품 개요 및 대상{#product-overview-and-audience}

이 안내서에서는 브라우저 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.

## 제품 개요 {#section_1C66E736CEFD4246B7C7C99AADD48118}

Adobe Primetime 소프트웨어 개발 키트(브라우저 TVSDK)는 브라우저 기반 비디오 플레이어 애플리케이션에 고급 비디오 재생 기능, 콘텐츠 보호 및 광고를 추가할 수 있는 툴킷입니다. 브라우저 TVSDK는 브라우저 기반 비디오 애플리케이션을 빌드하기 위한 JavaScript API를 제공하며 다음 모드에서 재생 지원을 포함합니다.

* HTML 5만
* 자동 플래시 대체 기능이 있는 HTML5
* 항상 Flash

이 릴리스에는 브라우저 TVSDK API 및 샘플 참조 구현이 포함되어 있습니다.

### UI 프레임워크

브라우저에 대한 JavaScript 기반 비디오 플레이어 애플리케이션의 UI 개발을 가속화하기 위해 브라우저 TVSDK에는 다음과 같은 작업을 수행하는 API로 구성된 UI 프레임워크가 포함되어 있습니다.

* 재생/일시 중지, 볼륨 등과 같은 기본 UI 컨트롤 포함
* DOM 구조를 직접 조작하지 않고도 고급 재생 UI 컨트롤을 쉽게 추가(또는 제거)할 수 있습니다
* 연결된 UI 컨트롤의 동작을 쉽게 구성할 수 있습니다
* 사용자 정의 UI 컨트롤 만들기
* 요구 사항에 따라 플레이어 UI 스킨

UI 프레임워크용 API에 대한 자세한 내용은 [브라우저 TVSDK 2.4용 UI 프레임워크](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html).

## 대상자 {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

이 안내서에서는 JavaScript를 사용하여 애플리케이션 및 비디오 플레이어를 개발하는 방법을 알고 있다고 가정합니다. 비디오 플레이어를 구현하고 브라우저 TVSDK 기능을 통합할 수 있습니다.

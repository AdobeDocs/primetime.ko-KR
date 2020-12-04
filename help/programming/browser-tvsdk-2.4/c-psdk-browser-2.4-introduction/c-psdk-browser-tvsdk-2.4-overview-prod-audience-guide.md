---
description: 이 안내서에서는 Browser TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.
seo-description: 이 안내서에서는 Browser TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.
seo-title: 제품 개요 및 고객
title: 제품 개요 및 고객
uuid: 902baabf-5e85-4d9c-8b5a-70ec0842e1bc
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# 제품 개요 및 대상{#product-overview-and-audience}

이 안내서에서는 Browser TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.

## 제품 개요 {#section_1C66E736CEFD4246B7C7C99AADD48118}

Adobe Primetime 소프트웨어 개발 키트(Browser TVSDK)는 브라우저 기반의 비디오 플레이어 애플리케이션에 고급 비디오 재생 기능, 컨텐츠 보호 및 광고를 추가할 수 있는 툴킷입니다. 브라우저 TVSDK는 브라우저 기반 비디오 애플리케이션을 구축할 수 있는 JavaScript API를 제공하며 다음 모드에서 재생 지원을 포함합니다.

* HTML5만 해당
* 자동 플래시 폴백을 사용하는 HTML5
* Flash은 항상

이 릴리스에는 Browser TVSDK API와 샘플 참조 구현이 포함되어 있습니다.

### UI 프레임워크

브라우저 TVSDK에는 브라우저용 JavaScript 기반 비디오 플레이어 응용 프로그램의 UI 개발 속도를 높이기 위해 API로 구성된 UI 프레임워크가 포함되어 있습니다.

* 재생/일시 정지, 볼륨 등과 같은 기본 UI 컨트롤 포함
* DOM 구조를 직접 조작하지 않고도 고급 재생 UI 컨트롤을 손쉽게 추가(또는 제거)
* 연관된 UI 컨트롤에 대한 동작을 쉽게 구성
* 사용자 정의 UI 컨트롤 만들기
* 요구 사항에 따라 플레이어 UI 스킨 지정

UI 프레임워크용 API에 대한 자세한 내용은 브라우저 TVSDK 2.4[용 UI 프레임워크를 참조하십시오.](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html)

## 대상 {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

이 안내서에서는 JavaScript를 사용하여 응용 프로그램 및 비디오 플레이어를 개발하는 방법을 알고 있다고 가정합니다. 비디오 플레이어를 구현하고 브라우저 TVSDK 기능을 통합할 수 있습니다.
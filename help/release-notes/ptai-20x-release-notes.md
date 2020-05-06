---
title: PTAI 20.3.3 릴리스 노트
description: PTAI 20.5.1 릴리스 노트는 2020년 Primetime 동적 광고 삽입에서 해결되고 알려진 문제를 담고 있습니다.
translation-type: tm+mt
source-git-commit: 2a5866be64895ba13994720bf943dc676c2595bf
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Primetime 동적 광고 삽입 20.5.1 릴리스 노트

동적 광고 삽입 20.5.1 릴리스 노트는 2020년 Primetime 동적 광고 삽입에서 새로운 기능 또는 변경된 기능, 해결된 문제 및 알려진 문제를 설명합니다.

## PTAI 20.5.1의 새로운 기능

**시기:** 2020년 5월 5일 화요일 오전 04:00부터 동부 오전 05:00까지

* If-Modified-Since 헤더가 전송될 때 올바른 CORS 헤더가 제공되도록 문제를 수정했습니다.

* CRS 대시보드의 버그 수정.

* 유지 관리 업데이트.

## 이전 릴리스에서 변경된 사항

### 버전 20.3.4

**시기:** 2020년 4월 1일 수요일 오전 03:00 ~ 오전 04:00 동부지역

* VOD/WebVTT에서 광고 삽입 후 자막이 동기화되지 않는 문제를 수정했습니다.

* 보안 업데이트.

### 버전 20.3.3

**시기:** 2020년 3월 26일 목요일 오전 03:00에서 동부 오전 04:00까지

* 이제 SSAI 4XX 및 5XX 응답에서 CORS 관련 헤더를 올바르게 제공하여 크로스 도메인 javascript/webview 클라이언트가 오류 응답을 성공적으로 읽을 수 있도록 합니다.

* 광고 서버로 전달될 때 IPv6 주소가 올바르게 URL로 인코딩되지 않았던 X-Forwarded-For 헤더의 문제를 수정했습니다.

* 특정 시나리오에서 EXT-X-MEDIA-SEQUENCE 번호가 잘못 증가하던 CMAF/demuxed 오디오 스트림 문제를 수정했습니다.

### 버전 20.1.3

**시기:** 2020년 1월 28일 화요일 오전 2시부터 오전 3시까지 동부시간

* **&quot;nbc&quot; CueFormat**&#x200B;에 대한 FER가 지원되는 VMAP을 사용하면 ptcueformat=nbc가 사용되고 스트림이 인큐 매니페스트 및 구이식 광고가 포함된 VOD 스트림인 경우 FER 스트림의 신호를 FW 타임라인 재정의 매개 변수로 변환할 수 있습니다.

* 타사 광고 공급자/CDN으로 전달하기 전에 HTTP 헤더에서 사용자-에이전트 필드의 기밀 정보를 가릴 수 있습니다.

* Auditude 및 기타 광고 공급자, CDN으로 전송하기 전에 &quot;user-agent&quot; HTTP 헤더에서 제어/인쇄할 수 없는 문자(32) 필터링 Auditude Ad-Call은 이러한 잘못된 헤더에 대해 실패하는 데 사용됩니다.

* NetStorage Group에서 이전 V1 개체를 제거하여 개체 수를 Akamai의 안전한 제한 내에 유지합니다.

## 해결된 문제

해결 방법이 보고된 문제와 연관된 경우 Zendesk 참조가 표시됩니다. 예: ZD#xxxxx.

**PTAI 20.3.3**

* 광고 서버로 전달될 때 IPv6 주소가 올바르게 URL로 인코딩되지 않았던 X-Forwarded-For 헤더의 문제.

* 특정 시나리오에서 EXT-X-MEDIA-SEQUENCE 번호가 특정 시나리오에서 잘못 증가되는 CMAF/demuxed 오디오 스트림 문제

## 알려진 문제 및 제한 사항

**PTAI 20.3.3**

새로운 제한이 추가되지 않았습니다.

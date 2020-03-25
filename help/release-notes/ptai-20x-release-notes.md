---
title: PTAI 20.3.3 릴리스 노트
description: PTAI 20.3.3 릴리스 노트는 2020년 Primetime 동적 광고 삽입의 새로운 기능 또는 변경된 사항과 해결되고 알려진 문제를 설명합니다.
translation-type: tm+mt
source-git-commit: ededb36a0b460fff4644a3716b36971ff9454c37

---


# Primetime 동적 광고 삽입 20.3.3 릴리스 노트

동적 광고 삽입 20.3.3 릴리스 노트는 2020년 Primetime 동적 광고 삽입에서 새로운 기능 또는 변경된 사항, 해결되고 알려진 문제를 설명합니다.

## PTAI 20.3.3의 새로운 기능

**시기:** 2020년 3월 26일 목요일 오전 03:00에서 동부 오전 04:00까지

* 이제 SSAI 4XX 및 5XX 응답에서 CORS 관련 헤더를 올바르게 제공하여 크로스 도메인 javascript/webview 클라이언트가 오류 응답을 성공적으로 읽을 수 있도록 합니다.

* X-Forwarded-For 헤더에서 IPv6 주소가 광고 서버로 전달될 때 올바르게 URL이 인코딩되지 않던 문제를 수정했습니다.

* 특정 시나리오에서 EXT-X-MEDIA-SEQUENCE 번호가 잘못 증가하던 CMAF/demuxed 오디오 스트림 문제를 수정했습니다.

## 이전 릴리스의 변경 사항

### 버전

**시기:**

### 버전

**시기:**

## 해결된 문제

해상도가 보고된 문제와 연결된 경우 Zendesk 참조가 표시됩니다. 예: ZD#xxxxx.

**PTAI 20.3.3**

* X-Forwarded-For 헤더에서 IPv6 주소가 광고 서버로 전달될 때 올바르게 URL이 인코딩되지 않는 문제가 해결되었습니다.

* 특정 시나리오에서 EXT-X-MEDIA-SEQUENCE 번호가 특정 시나리오에서 잘못 증가되는 CMAF/demuxed 오디오 스트림 문제

## 알려진 문제 및 제한 사항

**PTAI 20.3.3**

새로운 제한이 추가되지 않았습니다.

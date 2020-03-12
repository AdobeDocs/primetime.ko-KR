---
description: TVSDK를 사용하면 실시간 및 VOD(Video On Demand)를 위한 기본 재생 환경을 제어할 수 있습니다. TVSDK는 플레이어 사용자 인터페이스를 구성하는 데 사용할 수 있는 플레이어 인스턴스에 대한 메서드 및 속성을 제공합니다.
seo-description: TVSDK를 사용하면 실시간 및 VOD(Video On Demand)를 위한 기본 재생 환경을 제어할 수 있습니다. TVSDK는 플레이어 사용자 인터페이스를 구성하는 데 사용할 수 있는 플레이어 인스턴스에 대한 메서드 및 속성을 제공합니다.
seo-title: 유효한 상태 대기
title: 유효한 상태 대기
uuid: 22b68162-1625-4e8a-8566-b0c198155622
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 유효한 상태 대기 {#wait-for-a-valid-state}

TVSDK를 사용하면 실시간 및 VOD(Video On Demand)를 위한 기본 재생 환경을 제어할 수 있습니다. TVSDK는 플레이어 사용자 인터페이스를 구성하는 데 사용할 수 있는 플레이어 인스턴스에 대한 메서드 및 속성을 제공합니다.

대부분의 TVSDK 플레이어 메서드를 사용하려면 플레이어가 유효한 상태여야 합니다.
그 선수는 여러 가지 상태를 거친다. 플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필수 상태가 아닌 경우 많은 플레이어 메서드가 `IllegalStateException`발생합니다.

필요한 상태는 일반적으로 준비됩니다.

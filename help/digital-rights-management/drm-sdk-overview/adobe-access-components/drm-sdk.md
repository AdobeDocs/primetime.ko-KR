---
description: Primetime DRM의 기본 구성 요소는 Java SDK와 Flash Player 및 Adobe AIR 클라이언트 런타임 환경으로 구성됩니다.
title: Java SDK, Flash Player 및 Adobe AIR 클라이언트
exl-id: 5422d282-da9c-4810-a782-3c3af5fdeb3f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# ADOBE PRIMETIME DRM {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM은 서버 구현을 만들 수 있는 빌딩 블록을 제공하는 Java SDK로 제공됩니다. SDK를 사용하여 조직의 비즈니스 모델에 적합한 Primetime DRM 솔루션을 만들 수 있습니다.

SDK에 제공된 Java API는 다음 하위 섹션에 설명되어 있습니다.

## 장치 그룹 도메인 관리를 위한 Java API{#java-apis-for-managing-device-group-domains}

이러한 API는 서버가 장치 그룹 도메인에 가입하고 나가는 클라이언트 요청을 처리할 수 있도록 하는 데 사용됩니다.

장치 그룹 도메인은 서로 라이선스를 공유할 수 있는 장치의 논리적 컬렉션입니다. 이렇게 하려면 각 디바이스가 먼저 동일한 도메인에 가입/등록해야 합니다. 서버에서 실행되는 Primetime DRM SDK는 장치 도메인 가입(등록) 요청과 장치 도메인 탈퇴(등록 취소) 요청을 처리해야 합니다. 도메인에 가입되지 않은 장치에는 해당 장치에 바인딩된 라이선스가 발급되며, 이 라이선스는 다른 장치와 공유할 수 없습니다.

## 콘텐츠 보호를 위한 Java API{#java-apis-for-protecting-content}

이러한 API는 권한을 정의하고 배포할 콘텐츠를 준비하는 데 사용됩니다. 콘텐츠 보호 API는 다음과 같습니다.

* 정책 관리

   정책 관리 API는 콘텐츠에 적용할 정책을 만들고 수정하는 데 사용됩니다. 모든 사용 규칙을 가져오거나 설정하고, 사용자 지정 네임스페이스에서 추가 매개 변수를 허용하는 등 정책을 만들거나 업데이트할 수 있습니다.

* 컨텐츠 패키징

   컨텐츠 패키징 API는 컨텐츠를 암호화하고 패키징된 컨텐츠에서 메타데이터를 검색하는 데 사용됩니다.

## 라이선스 발급을 위한 Java API{#java-apis-for-issuing-licenses}

이러한 API는 클라이언트가 서버에서 라이선스를 요청할 때 사용됩니다. SDK는 클라이언트의 다음 요청을 지원합니다.

* 인증

   인증 API를 사용하여 인증 요청을 처리하고 인증 토큰을 생성할 수 있습니다.

* 라이선스 생성 및 획득

   라이선스 생성 및 획득 API는 사용자를 위한 라이선스를 생성하는 데 사용됩니다.

* Adobe AIR 버전 1.5 클라이언트 및 콘텐츠 지원

   이전 버전과의 호환성을 위해 SDK에는 AIR 버전 1.5 및 이전 버전의 클라이언트와 보호된 콘텐츠에서 사용하기 위해 만들어진 AIR 애플리케이션의 요청을 처리하는 API가 있습니다.

## 참조 구현 {#reference-implementation}

SDK에는 Java API를 사용하는 방법을 보여 주는 간단한 Adobe Primetime DRM 배포인 참조 구현이 포함되어 있습니다. 참조 구현은 Java API를 기반으로 하는 컨텐츠 패키징 및 정책 관리를 위한 라이선스 서버, 감시 폴더 패키저, Primetime DRM 관리자 AIR 애플리케이션 및 명령줄 도구를 제공합니다. Primetime DRM 참조 구현에 대한 자세한 내용은 콘텐츠 보호 를 참조하십시오.

---
description: TVSDK에서 MediaPlayerItemConfig 클래스를 사용하여 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-description: TVSDK에서 MediaPlayerItemConfig 클래스를 사용하여 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-title: 태그에 대한 구성 클래스 메서드
title: 태그에 대한 구성 클래스 메서드
uuid: b75aebac-4b94-4c42-bed4-3c17ad989cd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# {#config-class-methods-for-tags} 태그에 대한 구성 클래스 메서드

TVSDK에서 MediaPlayerItemConfig 클래스를 사용하여 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.

TVSDK는 스트림별 구성을 지정하지 않는 모든 미디어 스트림에 전역 구성을 자동으로 적용합니다.

`MediaPlayerItemConfig` 사용자 지정 태그를 관리하기 위해 다음 메서드를 노출합니다.

**특정 사용자 지정 태그 구독**

| <b>메서드</b> | <b>설명</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | 가입된 태그의 현재 목록을 검색합니다. |
| `public final void setSubscribedTags(String[] tags);` | 애플리케이션에 노출될 구독 태그 목록을 설정합니다.  애플리케이션이 `setAdTags`을(를) 통해 전송되는 모든 태그도 자동으로 구독됩니다. |

**기본 기회 탐지에 사용되는 광고 태그 사용자 정의**

| <b>메서드</b> | <b>설명</b> |
|--- |--- |
| `public final String[] getAdTags;` | 광고 태그의 현재 목록을 검색합니다. |
| `public final void setAdTags(String[] tags);` | 기본 기회 생성기에서 사용할 광고 태그 목록을 설정합니다. |

다음 사항을 기억하십시오.

* setter 메서드에서는 태그 매개 변수에 null 값을 포함할 수 없습니다.

   TVSDK에서 `IllegalArgumentException`을(를) throw합니다.
* 사용자 지정 태그 이름에는 `#` 접두사가 포함되어야 합니다.

   예를 들어 `#EXT-X-ASSET`은 올바른 사용자 지정 태그 이름이지만 `EXT-X-ASSET`이(가) 잘못되었습니다.

* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.
---
description: MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-description: MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-title: 태그에 대한 구성 클래스 메서드
title: 태그에 대한 구성 클래스 메서드
uuid: b75aebac-4b94-4c42-bed4-3c17ad989cd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 태그에 대한 구성 클래스 메서드 {#config-class-methods-for-tags}

MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.

TVSDK 파섹

`MediaPlayerItemConfig` 다음 메서드를 사용하여 사용자 지정 태그를 관리합니다.

**특정 사용자 정의 태그 구독**

| <b>메서드</b> | <b>설명</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | 현재 구독 태그 목록을 검색합니다. |
| `public final void setSubscribedTags(String[] tags);` | 애플리케이션에 노출될 구독 태그 목록을 설정합니다.  또한 애플리케이션은 를 통해 전송되는 모든 태그도 자동으로 구독됩니다 `setAdTags`. |

**기본 기회 탐지기에서 사용하는 광고 태그 사용자 정의**

| <b>메서드</b> | <b>설명</b> |
|--- |--- |
| `public final String[] getAdTags;` | 광고 태그의 현재 목록을 검색합니다. |
| `public final void setAdTags(String[] tags);` | 기본 기회 생성기에서 사용할 광고 태그 목록을 설정합니다. |

다음 사항을 기억하십시오.

* setter 메서드는 태그 매개 변수에 null 값을 포함할 수 없습니다.

   이 경우 TVSDK에서 TV가 `IllegalArgumentException`발생합니다.
* 사용자 지정 태그 이름에는 `#` 접두사가 포함되어야 합니다.

   예를 들어 `#EXT-X-ASSET` 는 올바른 사용자 지정 태그 이름이지만 `EXT-X-ASSET` 잘못되었습니다.

* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.
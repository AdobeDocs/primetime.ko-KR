---
description: MediaPlayerItemConfig 클래스 또는 MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-description: MediaPlayerItemConfig 클래스 또는 MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-title: 태그에 대한 구성 클래스 메서드
title: 태그에 대한 구성 클래스 메서드
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 태그{#config-class-methods-for-tags}에 대한 구성 클래스 메서드

MediaPlayerItemConfig 클래스 또는 MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.

TVSDK는 스트림별 구성을 지정하지 않는 모든 미디어 스트림에 전역 구성을 자동으로 적용합니다.

`PSDKConfig` 및 `MediaPlayerItemConfig` 모두 이러한 메서드를 노출하여 사용자 지정 태그를 관리합니다.

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>특정 사용자 지정 태그 구독</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function get subscribeTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> 가입된 태그의 현재 목록을 검색합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set subscribeTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2">애플리케이션에 노출될 구독 태그 목록을 설정합니다. <p>애플리케이션이 <span class="codeph"> adTags</span>를 통해 전송되는 모든 태그도 자동으로 구독됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>기본 기회 탐지에 사용되는 광고 태그 사용자 정의  </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function get adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> 광고 태그의 현재 목록을 검색합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> 기본 기회 생성기에서 사용할 광고 태그 목록을 설정합니다. </td> 
  </tr> 
 </tbody> 
</table>

다음 사항을 기억하십시오.

* setter 메서드에서는 태그 매개 변수에 null 값을 포함할 수 없습니다.

   TVSDK에서 `IllegalArgumentException`을(를) throw합니다.
* 사용자 지정 태그 이름에는 # 접두사가 포함되어야 합니다.

   예를 들어 `#EXT-X-ASSET`은 올바른 사용자 지정 태그 이름이지만 `EXT-X-ASSET`이(가) 잘못되었습니다.
* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.


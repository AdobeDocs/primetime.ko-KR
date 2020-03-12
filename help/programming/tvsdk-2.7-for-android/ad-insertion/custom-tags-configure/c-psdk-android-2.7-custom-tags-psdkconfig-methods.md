---
description: MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-description: MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.
seo-title: 태그에 대한 구성 클래스 메서드
title: 태그에 대한 구성 클래스 메서드
uuid: 64284876-1f31-47e0-a99b-3bfe17e10707
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 태그에 대한 구성 클래스 메서드 {#config-class-methods-for-tags}

MediaPlayerItemConfig 클래스를 사용하여 TVSDK에서 사용자 지정 태그 이름을 전체적으로 구성할 수 있습니다.

TVSDK 파섹

`MediaPlayerItemConfig` 다음 메서드를 사용하여 사용자 지정 태그를 관리합니다.

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>특정 사용자 정의 태그 구독</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>현재 구독 태그 목록을 검색합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>애플리케이션에 노출될 구독 태그 목록을 설정합니다. </p> <p>또한 애플리케이션은 setAdTags를 통해 전송된 모든 태그에 자동으로 <span class="codeph"> 구독됩니다 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>기본 기회 탐지기에서 사용하는 광고 태그 사용자 정의</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags; </span> </td> 
   <td colname="col2"> <p>광고 태그의 현재 목록을 검색합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>기본 기회 생성기에서 사용할 광고 태그 목록을 설정합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 사항을 기억하십시오.

* setter 메서드는 태그 매개 변수에 null 값을 포함할 수 없습니다.

   이 경우 TVSDK에서 TV가 `IllegalArgumentException`발생합니다.
* 사용자 지정 태그 이름에는 `#` 접두사가 포함되어야 합니다.

   예를 들어 `#EXT-X-ASSET` 는 올바른 사용자 지정 태그 이름이지만 `EXT-X-ASSET` 잘못되었습니다.

* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.

---
description: MediaPlayerItemConfig 클래스를 사용하여 전역적으로 TVSDK에서 사용자 지정 태그 이름을 구성하거나, MediaPlayerItemConfig 클래스를 사용하여 스트림 기반으로 사용자 지정 태그 이름을 구성할 수 있습니다.
title: 태그에 대한 클래스 메서드 구성
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 태그에 대한 클래스 메서드 구성{#config-class-methods-for-tags}

MediaPlayerItemConfig 클래스를 사용하여 전역적으로 TVSDK에서 사용자 지정 태그 이름을 구성하거나, MediaPlayerItemConfig 클래스를 사용하여 스트림 기반으로 사용자 지정 태그 이름을 구성할 수 있습니다.

TVSDK는 스트림별 구성을 지정하지 않는 모든 미디어 스트림에 전역 구성을 자동으로 적용합니다.

모두 `PSDKConfig` 및 `MediaPlayerItemConfig` 다음 메서드를 노출하여 사용자 지정 태그를 관리합니다.

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>특정 사용자 정의 태그 구독</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public 함수 get subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> 구독한 태그의 현재 목록을 검색합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 공용 함수 집합 subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2">애플리케이션에 노출될 구독한 태그 목록을 설정합니다. <p>또한 응용 프로그램은 다음을 통해 전송되는 모든 태그에 자동으로 가입됩니다. <span class="codeph"> adtags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>기본 영업 기회 감지기에 사용되는 광고 태그 사용자 지정 </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public 함수 get adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> 현재 광고 태그 목록을 검색합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 공용 함수 집합 adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> 기본 영업 기회 생성기에 사용될 광고 태그 목록을 설정합니다. </td> 
  </tr> 
 </tbody> 
</table>

다음 사항을 기억하십시오.

* setter 메서드는 태그 매개 변수에 null 값을 포함할 수 없습니다.

  발견된 경우 TVSDK는 `IllegalArgumentException`.
* 사용자 지정 태그 이름에는 # 접두사가 있어야 합니다.

  예를 들어, `#EXT-X-ASSET` 은(는) 올바른 사용자 지정 태그 이름이지만, `EXT-X-ASSET` 은(는) 잘못되었습니다.
* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.

---
description: MediaPlayerItemConfig 클래스를 사용하여 스트림에서 사용자 지정 태그 이름을 구성할 수 있습니다.
seo-description: MediaPlayerItemConfig 클래스를 사용하여 스트림에서 사용자 지정 태그 이름을 구성할 수 있습니다.
seo-title: 태그에 대한 구성 클래스 메서드
title: 태그에 대한 구성 클래스 메서드
uuid: 222a0349-58d5-4bf3-9d03-e5920610faf5
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661

---


# 태그에 대한 구성 클래스 메서드{#config-class-methods-for-tags}

MediaPlayerItemConfig 클래스를 사용하여 스트림에서 사용자 지정 태그 이름을 구성할 수 있습니다.

새로 만들려면 `MediaPlayerItemConfig`다음을 수행하십시오.

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

다음은 이 방법을 사용하여 사용자 지정 태그를 관리하는 방법에 대한 `MediaPlayerItemConfig` 정보입니다.

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>특정 사용자 정의 태그 구독</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>현재 구독 태그 목록을 검색합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>애플리케이션에 노출된 구독 태그 목록을 설정합니다. </p> <p>또한 애플리케이션은 광고 태그를 통해 전송되는 모든 태그에 자동으로 <span class="codeph"> 구독됩니다 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>기본 기회 탐지기에서 사용하는 광고 태그 사용자 정의 </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>광고 태그의 현재 목록을 검색합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>기본 기회 생성기에서 사용할 광고 태그 목록을 설정합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 사항을 기억하십시오.

* 사용자 지정 태그 이름에는 `#` 접두사가 포함되어야 합니다.

   예를 들어 `#EXT-X-ASSET` 는 올바른 사용자 지정 태그 이름이지만 `EXT-X-ASSET` 잘못되었습니다.

* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.


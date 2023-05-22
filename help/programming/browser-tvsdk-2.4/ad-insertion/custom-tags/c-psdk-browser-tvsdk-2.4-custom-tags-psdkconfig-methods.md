---
description: MediaPlayerItemConfig 클래스를 사용하여 스트림에서 사용자 지정 태그 이름을 구성할 수 있습니다.
title: 태그에 대한 클래스 메서드 구성
exl-id: 864d5c35-2b26-447b-8134-414e82096f18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 태그에 대한 클래스 메서드 구성{#config-class-methods-for-tags}

MediaPlayerItemConfig 클래스를 사용하여 스트림에서 사용자 지정 태그 이름을 구성할 수 있습니다.

새로 만들려면 `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

다음은 어떻게 `MediaPlayerItemConfig` 메서드는 사용자 지정 태그를 관리하는 데 사용됩니다.

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
   <td colname="col2"> <p>구독한 태그의 현재 목록을 검색합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>애플리케이션에 노출된 구독한 태그 목록을 설정합니다. </p> <p>또한 애플리케이션은 을 통해 전송되는 모든 태그에 자동으로 가입됩니다. <span class="codeph"> adtags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>기본 영업 기회 감지기에 사용되는 광고 태그 사용자 지정 </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>현재 광고 태그 목록을 검색합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>기본 영업 기회 생성기에서 사용할 광고 태그 목록을 설정합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 사항을 기억하십시오.

* 사용자 지정 태그 이름에는 `#` 접두사입니다.

   예를 들어, `#EXT-X-ASSET` 은(는) 올바른 사용자 지정 태그 이름이지만, `EXT-X-ASSET` 은(는) 잘못되었습니다.

* 미디어 스트림이 로드된 후에는 구성을 변경할 수 없습니다.

---
description: ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. 브라우저 TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.
title: ID3 태그
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# ID3 태그{#id-tags}

ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. 브라우저 TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.

기본 HLS 스트림에서 새 ID3 메타데이터가 발견되면 브라우저 TVSDK가 `AdobePSDK.TimedMetadataEvent` 이벤트를 트리거합니다.

ID3용 `TimedMetadata` 객체에는 다음 속성이 있습니다.

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 속성 이름 </th> 
   <th colname="col2" class="entry"> 세부 정보 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> type  </span> </p> </td> 
   <td colname="col2"> <p><span class="codeph"> TimedMetadata </span> 객체의 유형입니다. </p> <p>ID3 메타데이터의 경우 이 값은 <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> time  </span> </p> </td> 
   <td colname="col2"> <p> 이 시간 지정 메타데이터가 검색된 플레이어 시간입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id  </span> </p> </td> 
   <td colname="col2"> <p><span class="codeph"> TimedMetadata </span> 개체의 ID입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> name  </span> </p> </td> 
   <td colname="col2"> <p><span class="codeph"> TimedMetadata </span> 개체의 이름입니다. ID3 메타데이터의 경우 값은 "ID3"입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 콘텐트  </span> </p> </td> 
   <td colname="col2"> <p>시간 지정 메타데이터 컨텐츠. ID3 태그의 경우 이 값은 직렬화된 바이트 배열을 나타냅니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 메타데이터  </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata  </span> 처리된 정보. 이 정보는  <span class="codeph"> AdobePSDK.Metadata </span> 로 ID3 프레임이 저장됩니다. </p> <p> <p>참고: Safari <span class="codeph"> 비디오 </span> 태그의 경우, ID3 태그의 특정 프레임 데이터가 <span class="codeph"> AdobePSDK.Metadata </span> 개체를 통해 객체 형태로 노출되지만 다른 브라우저의 경우 ID3 태그의 프레임 데이터는 <span class="codeph"> AdobePSDK.Metadata </span>를 통해 바이트 배열의 형태로 노출됩니다.&gt; 개체. </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

응용 프로그램에서 `TimedMetadata`에 저장되는 다양한 ID3 태그를 다음 두 가지 방법으로 검색할 수 있습니다.

* AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE 이벤트 리스너입니다.

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var mediaPlayer = new AdobePSDK.MediaPlayer(); 
   mediaPlayer.addEventListener( AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE ,function(event){ 
       var td = event.timedMetadata; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   }); 
   ```

* `MediaPlayerItem`의 `timedMetadata` 속성 사용

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var timedMetadataList = player.currentItem.timedMetadata; 
   for(var i = 0; i < timedMetadataList.length; i++){ 
       var td = timedMetadataList[i]; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   } 
   ```


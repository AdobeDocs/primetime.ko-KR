---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
seo-description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
seo-title: 볼륨 제어 제공
title: 볼륨 제어 제공
uuid: c51e99b6-efd1-414e-9ef7-77bd53e0d6c0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 볼륨 제어 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. MediaPlayer 인스턴스가 이 명령의 유효한 상태가 될 때까지 기다립니다.

   RELEASED를 제외한 모든 상태는 유효합니다.
1. 인스턴스에서 볼륨 세트 메서드를 호출하여 오디오 볼륨을 설정합니다. `MediaPlayer`

   ```
   public function set volume(value:Number):void
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현된 요청된 볼륨을 나타냅니다. 여기서 0은 묵음이고 1은 최대 볼륨입니다.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 지정된 볼륨이 </th> 
      <th colname="col2" class="entry"> 결과 볼륨은 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 0 미만 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 0에서 1 사이 </td> 
      <td colname="col2"> 지정된 볼륨 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 1보다 큼 </td> 
      <td colname="col2"> 값을 100으로 나눈 후 다음 값 중 하나로 설정합니다. 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">0과 1 사이의 결과입니다. </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 결과가 1보다 큰 경우 </li> 
      </ul> <p>팁: 이 로직은 볼륨 값이 0에서 100까지인 <span class="codeph">구문/primetime-sdk-name</span>이전 버전을 기준으로 클라이언트에서 제공되는 값을 처리합니다. </p> </td> 
   </tr> 
   </tbody> 
   </table>

---
description: 우선 순위 규칙은 VAST 파섹/VMAP 응답에서 재생하도록 선택할 광고 크리에이티브의 우선 순위 순서를 정의합니다.
keywords: priority rule;creative selection rules
seo-description: 우선 순위 규칙은 VAST 파섹/VMAP 응답에서 재생하도록 선택할 광고 크리에이티브의 우선 순위 순서를 정의합니다.
seo-title: 우선 순위 규칙
title: 우선 순위 규칙
uuid: 86b9d654-c85c-45de-a512-969234c56bef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 우선 순위 규칙 {#priority-rules}

우선 순위 규칙은 VAST 파섹/VMAP 응답에서 재생하도록 선택할 광고 크리에이티브의 우선 순위 순서를 정의합니다.

## 우선 순위 규칙에는 다음과 같은 속성과 가능한 값이 있습니다.

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>키</b></th> 
   <th class="entry"><b>유형</b></th> 
   <th class="entry"><b>값</b></th> 
   <th class="entry"><b>설명</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 우선 순위</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> 재생을 위해 소스 크리에이티브를 선택해야 하는 우선 순위를 정의하는 소문자 MIME 유형의 배열입니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 호스트</span></td> 
   <td>현재 <span class="codeph"> 호스트만</span> 지원됩니다. 이 속성은 <span class="codeph"> 일치</span> 및 <span class="codeph"> 값이</span> 정의된 경우 존재해야 합니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> multiple</span></td> 
   <td>가능한 값:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - 같음</li> 
     <li><span class="codeph"> ne</span> - 같지 않음</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span> - 포함하지 않음</li> 
     <li><span class="codeph"> sw</span> - 다음으로 시작</li> 
     <li><span class="codeph"> new</span> - 다음으로 끝남</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 우선 순위</span></td> 
   <td>값은 항상 <span class="codeph"> 우선 순위여야 합니다.</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> <p>TVSDK는 소스 크리에이티브 항목의 <span class="codeph"> 일치</span> <span class="codeph"></span> 속성을 사용하고 이 배열에 정의된 값과 일치시킵니다.</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> stream</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td></td> 
   <td> <p>값은 <span class="codeph"> vod</span> 또는 <span class="codeph"> live일 수 있습니다.</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```

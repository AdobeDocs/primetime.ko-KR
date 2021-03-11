---
description: 표준화 규칙은 VAST/VMAP 응답에서 얻은 소스 크리에이티브 URL에 적용할 URL 변형을 정의합니다.
keywords: 규칙 정규화;크리에이티브 선택 규칙
title: 규칙 표준화
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---


# 규칙 표준화 {#normalize-rules}

표준화 규칙은 VAST/VMAP 응답에서 얻은 소스 크리에이티브 URL에 적용할 URL 변형을 정의합니다.

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 표준화</span></td> 
   <td>값은 항상 <span class="codeph"> 정규화</span>여야 합니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 호스트</span></td> 
   <td>현재 <span class="codeph"> 호스트</span>만 지원됩니다. <span class="codeph">이(가) </span> 및 <span class="codeph"> 값</span> 특성이 정의된 경우 이 특성이 있어야 합니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
   <td>가능한 값:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - 같음</li> 
     <li><span class="codeph"> ne</span>  - 같지 않음</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span>  - 포함하지 않음</li> 
     <li><span class="codeph"> sw</span>  - 다음으로 시작</li> 
     <li><span class="codeph"> 새</span>  - 다음으로 끝남</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> value</span></td> 
   <td><span class="codeph"> 배열</span></td> 
   <td></td> 
   <td>TVSDK는 소스 크리에이티브의 <span class="codeph"> 항목</span>에 <span class="codeph"> 일치</span> 특성을 사용하고 이 배열에 정의된 값과 일치시킵니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> find</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> 일치시킬 소스 크리에이티브 URL에 적용할 일반 표현식.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> 일치에 따라 대체할 소스 크리에이티브 URL에 적용할 일반 표현식.</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```

---
description: 표준화 규칙은 VAST 파섹/VMAP 응답에서 얻은 소스 크리에이티브 URL에 적용할 URL 변환을 정의합니다.
keywords: normalize rule;creative selection rules
seo-description: 표준화 규칙은 VAST 파섹/VMAP 응답에서 얻은 소스 크리에이티브 URL에 적용할 URL 변환을 정의합니다.
seo-title: 규칙 표준화
title: 규칙 표준화
uuid: ae0364d2-23e2-48d6-b9b6-869cd163080d
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 규칙 표준화 {#normalize-rules}

표준화 규칙은 VAST 파섹/VMAP 응답에서 얻은 소스 크리에이티브 URL에 적용할 URL 변환을 정의합니다.

## 표준화 규칙에는 다음과 같은 특성과 가능한 값이 있습니다.

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> 키</th> 
   <th class="entry"> 유형</th> 
   <th class="entry"> 값</th> 
   <th class="entry"> 설명</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 표준화</span></td> 
   <td>값은 항상 <span class="codeph"> 정규화되어야</span>합니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 호스트</span></td> 
   <td>현재 <span class="codeph"> 호스트만</span> 지원됩니다. 이 속성은 <span class="codeph"> 일치</span> 및 <span class="codeph"> 값이</span> 정의된 경우 존재해야 합니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td>TVSDK는 소스 크리에이티브 항목의 <span class="codeph"> 일치</span> <span class="codeph"></span> 속성을 사용하고 이 배열에 정의된 값과 일치시킵니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> find</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> 일치시킬 소스 크리에이티브 URL에 적용할 정규 표현식.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> 일치에 따라 대체할 소스 크리에이티브 URL에 적용할 정규 표현식.</td> 
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


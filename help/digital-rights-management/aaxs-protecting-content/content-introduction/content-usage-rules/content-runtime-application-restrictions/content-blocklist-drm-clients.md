---
title: 보호된 콘텐츠에 대한 액세스가 제한되는 DRM 클라이언트 차단 목록
description: 보호된 콘텐츠에 대한 액세스가 제한되는 DRM 클라이언트 차단 목록
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# 보호된 콘텐츠에 대한 액세스가 제한되는 DRM 클라이언트 차단 목록 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe 액세스 DRM 모듈 버전이 보호된 콘텐츠에 액세스하지 못하도록 제한되었습니다.**

콘텐츠에 액세스할 수 없는 DRM 클라이언트를 지정합니다. DRM 클라이언트 버전 및 플랫폼에서 지정합니다.

사용 사례: 보안 침해가 발생한 경우 라이선스 획득 및 콘텐츠 재생에 필요한 최소 버전으로 DRM 클라이언트의 최신 버전을 지정할 수 있습니다. 라이센스 서버는 라이센스를 발행하기 전에 라이센스 요청을 하는 DRM 클라이언트가 버전 요구 사항을 충족하는지 확인합니다. 또한 DRM 클라이언트는 콘텐츠를 재생하기 전에 라이센스에서 DRM 버전을 확인합니다. 라이선스를 다른 컴퓨터로 전송할 수 있는 도메인의 경우 이 클라이언트 검사가 필요합니다.

DRM 클라이언트 버전은 다음 표에 지정된 속성에 의해 식별될 수 있습니다.

| **속성** | **지원되는 값** | **일치 기준** | **설명** |
|---|---|---|---|
| 환경 | &quot;PC&quot;, &quot;PortingKit&quot; | 정확한 일치 | 클라이언트가 데스크탑 또는 기타 장치에서 실행 중인지 식별합니다. |
| OS | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | 정확한 일치 | 플랫폼 |
| 아키텍처 | “32”, “64” | 정확한 일치 | 32비트 또는 64비트 |
| 화면 유형 | &quot;PC&quot;, &quot;모바일&quot;, &quot;TV&quot; | 정확한 일치 | |
| 런타임 버전 | 유효한 버전 번호입니다. 예를 들어 &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot; 등이 있습니다. | 클라이언트 버전이 지정된 버전보다 작거나 같은 경우 일치합니다. | 버전 번호는 숫자와 마침표의 조합으로 지정됩니다(&quot;.&quot;). 어떤 길이든. |
| DRM 라이브러리 버전 | 유효한 버전 번호입니다. 예를 들어 &quot;2.0.0&quot;입니다. | 클라이언트 버전이 지정된 버전보다 작거나 같은 경우 일치합니다. | 버전 번호는 숫자와 마침표의 조합으로 지정됩니다(&quot;.&quot;). 어떤 길이든. |
| OEM 공급업체 | OEM 공급업체 문자열 | 정확한 일치 | 이식 키트를 사용하는 장치의 OEM 공급업체 식별 문자열. |
| 모델 | 모델 문자열입니다. 예: &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | 정확한 일치 | 이식 키트를 사용하는 장치에 대한 장치 모델 식별 문자열입니다. |

>[!NOTE]
>
>차단 목록에서 엔트리를 지정할 때 이전 표에서 언급된 속성 중 하나 이상에 대해 값들을 설정할 수 있다. 지정되지 않은 모든 속성은 와일드카드로 처리됩니다. DRM 클라이언트가 차단 목록 항목에 지정된 모든 값과 일치하면 해당 클라이언트가 보호된 콘텐츠에 액세스하지 못할 수 있습니다.

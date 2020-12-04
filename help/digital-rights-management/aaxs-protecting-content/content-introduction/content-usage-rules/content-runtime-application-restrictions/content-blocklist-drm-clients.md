---
seo-title: 보호된 콘텐츠에 대한 액세스가 제한된 DRM 클라이언트의 차단 목록
title: 보호된 콘텐츠에 대한 액세스가 제한된 DRM 클라이언트의 차단 목록
uuid: c05aa6f8-32d9-42aa-a9c5-0d0629d49778
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# 보호된 내용 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}에 액세스할 수 없는 DRM 클라이언트의 차단 목록

**Adobe 보호된 콘텐츠에 액세스할 수 없도록 제한된 DRM 모듈 버전.**

콘텐츠에 액세스할 수 없는 DRM 클라이언트를 지정합니다. DRM 클라이언트 버전 및 플랫폼에서 지정되었습니다.

사용 사례 예:보안 문제가 발생하는 경우 라이선스 취득 및 컨텐츠 재생에 필요한 최소 버전으로 최신 버전의 DRM 클라이언트를 지정할 수 있습니다. 라이센스 서버는 라이센스 요청을 수행하는 DRM 클라이언트가 라이센스를 발급하기 전에 버전 요구 사항을 충족하는지 확인합니다. 또한 DRM 클라이언트는 콘텐츠를 재생하기 전에 라이선스의 DRM 버전을 확인합니다. 라이센스를 다른 시스템으로 전송할 수 있는 도메인의 경우 이 클라이언트 확인이 필요합니다.

DRM 클라이언트 버전은 다음 표에 지정된 속성으로 식별할 수 있습니다.

| **속성** | **지원되는 값** | **일치 기준** | **설명** |
|---|---|---|---|
| 환경 | &quot;PC&quot;, &quot;PortingKit&quot; | 정확히 일치 | 클라이언트가 데스크탑에서 실행되고 있는지 또는 다른 장치에서 실행되고 있는지 확인합니다. |
| OS | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | 정확히 일치 | 플랫폼 |
| 건축 | &quot;32&quot;, &quot;64&quot; | 정확히 일치 | 32비트 또는 64비트 |
| 화면 유형 | &quot;PC&quot;, &quot;모바일&quot;, &quot;TV&quot; | 정확히 일치 |  |
| 런타임 버전 | 유효한 버전 번호입니다. 예: &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot; 등 | 클라이언트 버전이 지정된 버전보다 작거나 같은 경우 일치합니다. | 버전 번호는 숫자 및 마침표(&quot;.&quot;)의 조합으로 지정됩니다. 모든 길이에 |
| DRM 라이브러리 버전 | 유효한 버전 번호입니다. 예: &quot;2.0.0&quot;. | 클라이언트 버전이 지정된 버전보다 작거나 같은 경우 일치합니다. | 버전 번호는 숫자 및 마침표(&quot;.&quot;)의 조합으로 지정됩니다. 모든 길이에 |
| OEM 공급업체 | OEM 공급업체 문자열 | 정확히 일치 | OEM 포팅 키트를 사용하는 장치에 대한 공급업체 식별 문자열. |
| 모델 | 모델 문자열. 예: &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | 정확히 일치 | 포팅 키트를 사용하는 장치의 장치 모델 식별 문자열. |

>[!NOTE]
>
>차단 목록에서 항목을 지정할 때 이전 표에 언급된 하나 이상의 속성에 대해 값을 설정할 수 있습니다. 지정되지 않은 속성은 모두 와일드카드로 처리됩니다. DRM 클라이언트가 차단 목록 항목에 지정된 모든 값과 일치하는 경우 해당 클라이언트가 보호된 콘텐츠에 액세스할 수 없습니다.


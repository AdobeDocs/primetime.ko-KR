---
title: 장치 ID가 없는 클라이언트 없는 API 흐름
description: 장치 ID가 없는 클라이언트 없는 API 흐름
exl-id: 6549a6d6-03a9-4d95-99fb-d3ada832323d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 장치 ID가 없는 클라이언트 없는 API 흐름 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

</br>


## 문제

일부 스마트 장치 앱에서는 고유한 장치 ID를 제공할 수 없습니다.  deviceId는 필수 매개 변수이므로 전달되지 않으면 서비스가 400 오류를 반환합니다.


## 임시 솔루션/해결 방법

장치 ID가 없는 클라이언트의 경우:

1. 를 사용하여 처음으로 등록 코드 서비스를 호출합니다. `deviceId=dummy`
1. 응답에서 UUID를 추출합니다. UUID는 등록 코드 응답(XML 및 JSON 응답 형식)의 &quot;id&quot; 요소에서 사용할 수 있습니다.
1. 등록 서비스에 다시 전화합니다. 이번에는 통과 `deviceId=<uuid obtained in step #2>`
1. 3단계에서 얻은 등록 코드를 콘솔 UI에 표시


이 단계가 완료되면 Adobe Primetime 인증은 UUID를 장치 ID로 사용합니다. 이 장치 ID(UUID)를 장치의 로컬 저장소에 저장합니다. 사용자가 새 등록 코드를 생성하는 경우 1~4단계를 다시 실행한 다음 이전에 저장된 UUID(장치 ID)를 새 ID로 교체해야 합니다.



## 영구 솔루션

Adobe은 다음을 수행하여 향후 릴리스에서 이를 변경합니다. `deviceId` regCode를 만들고 대신 UUID를 토큰 키로 사용할 때의 선택적 페이로드 `deviceId`, 다음과 같은 경우 `deviceId` 이(가) 없습니다.

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->

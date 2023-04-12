---
title: 장치 ID가 없는 경우 Clientless API 흐름
description: 장치 ID가 없는 경우 Clientless API 흐름
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 장치 ID가 없는 경우 Clientless API 흐름 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>


## 문제

일부 스마트 장치 앱에서는 고유한 장치 ID를 제공할 수 없습니다.  deviceId는 필수 매개 변수이므로 전달되지 않으면 서비스가 400 오류를 반환합니다.


## 임시 솔루션 / 해결 방법

장치 ID가 없는 클라이언트의 경우:

1. 를 사용하여 처음으로 등록 코드 서비스를 호출합니다. `deviceId=dummy`
1. 응답에서 UUID를 추출합니다. UUID는 등록 코드 응답(XML 및 JSON 응답 형식)의 &quot;id&quot; 요소에서 사용할 수 있습니다.
1. 다시 등록 서비스에 전화하세요. 이번엔 지나가세요 `deviceId=<uuid obtained in step #2>`
1. 콘솔 UI에서 3단계에서 얻은 등록 코드를 표시합니다


이 단계를 완료하면 Adobe Primetime 인증에서는 UUID를 장치 ID로 사용합니다. 이 장치 ID(UUID)를 장치의 로컬 저장소에 저장합니다. 사용자가 새 등록 코드를 생성하는 경우 1단계부터 4단계까지 다시 실행한 다음 이전에 저장된 UUID(Device ID)를 새로운 것으로 교체해야 합니다.



## 영구 솔루션

Adobe은 다음 방법으로 향후 릴리스에서 이 내용을 변경할 것입니다 `deviceId` reg 코드를 만들 때 선택적 페이로드를 생성하고 UUID를 대신 토큰 키로 사용합니다. `deviceId`, when `deviceId` 이 없습니다.

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->
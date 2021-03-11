---
title: 샘플 클라이언트 요청
description: 샘플 클라이언트 요청
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# 샘플 클라이언트 요청{#sample-client-requests}

Charles Proxy 또는 Wireshark와 같은 도구를 사용하여 샘플 클라이언트 요청의 라이브러리를 수집할 수 있습니다. 개인화 전송 자격 증명을 사용하여 개인화 서버가 설정된 후에 클라이언트 요청을 캡처해야 합니다. 그런 다음 이러한 클라이언트 요청(*말림* 또는 다른 도구를 통해)을 Indiation Server의 끝점으로 보내 서버가 제대로 작동하고 있는지 확인할 수 있습니다. 예:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

서버 구성 변경 또는 ECI/CRL 업데이트 후에 이러한 요청을 다시 전송할 수도 있습니다.

성공적인 개인화 트랜잭션으로 개인화 통계 페이지를 적절히 업데이트해야 합니다.

---
title: 샘플 클라이언트 요청
description: 샘플 클라이언트 요청
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 샘플 클라이언트 요청{#sample-client-requests}

Charles Proxy 또는 Wireshark와 같은 도구를 사용하여 샘플 클라이언트 요청 라이브러리를 수집할 수 있습니다. 개인화 전송 자격 증명을 사용하여 개인화 서버가 설정된 후 클라이언트 요청을 캡처해야 합니다. 그런 다음 이러한 클라이언트 요청을 (를 통해) 보낼 수 있습니다. *컬* 또는 다른 도구)를 사용하여 Individualization Server의 끝점으로 이동하여 서버가 제대로 실행되고 있는지 확인합니다. 예:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

서버 구성이 변경되거나 ECI/CRL이 업데이트된 후 이러한 요청을 다시 보낼 수도 있습니다.

또한 성공적인 개별화 트랜잭션과 함께 개별화 통계 페이지를 적절하게 업데이트해야 합니다.

---
seo-title: 크로스 도메인 정책 파일
title: 크로스 도메인 정책 파일
uuid: fc05aa5e-6fbd-445f-a22a-f795d5a0b3ad
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 크로스 도메인 정책 파일 {#crossdomain-policy-file}

라이센스 서버가 비디오 재생 SWF와 다른 도메인에 호스팅되는 경우 SWF가 라이센스 서버의 라이센스를 요청하도록 허용하려면 크로스 도메인 정책 파일(crossdomain.xml)이 필요합니다. 크로스 도메인 정책 파일은 다른 도메인에서 제공되는 SWF 파일에서 데이터와 문서를 사용할 수 있음을 나타내는 방법을 제공하는 XML 파일입니다. 라이센스 서버의 도메인 간 정책 파일에 지정된 도메인에서 제공된 모든 SWF 파일은 해당 라이센스 서버의 데이터나 자산에 액세스할 수 있습니다.

Adobe은 개발자가 트러스트된 도메인만 라이센스 서버에 액세스하고 웹 서버의 라이센스 하위 디렉토리에 대한 액세스를 제한함으로써 크로스 도메인 정책 파일을 배포할 때 모범 사례를 따를 것을 권장합니다.

크로스 도메인 정책 파일에 대한 자세한 내용은 다음 위치를 참조하십시오.

* 웹 사이트 컨트롤(정책 파일)
* 도메인 간 정책 파일 사양:[https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)


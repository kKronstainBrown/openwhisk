---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-12"

keywords: faq, runtimes, actions, memory, monitoring

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# FAQ
{: #faq}

이 FAQ에서는 {{site.data.keyword.openwhisk_short}} 서비스에 대한 일반적인 질문의 답을 제공합니다.
{: shortdesc}


## 지원되는 언어 런타임은 무엇입니까?
{: #runtimes}
{: faq}

다음 언어가 지원됩니다. 

<table>
  <tr>
    <th id="language-col">언어</th>
    <th id="kind-identifier-col">유형 ID</th>
  </tr>
  <tr>
    <td id="language-col-nodejs" headers="language-col"> Node.js</td>
    <td headers="kind-identifier-col language-col-nodejs"><code>nodejs:6</code>, <code>nodejs:8</code></td>
  </tr>
  <tr>
    <td id="language-col-python" headers="language-col">Python</td>
    <td headers="kind-identifier-col language-col-python"><code>python:3.7</code>, <code>python:3.6</code></td>
  </tr>
  <tr>
    <td id="language-col-swift" headers="language-col">Swift</td>
    <td headers="kind-identifier-col language-col-swift"><code>swift:4.1</code>, <code>swift:3.1.1</code></td>
  </tr>
  <tr>
    <td id="language-col-php" headers="language-col">PHP</td>
    <td headers="kind-identifier-col language-col-php"><code>php:7.2</code>, <code>php:7.1</code></td>
  </tr>
  <tr>
    <td id="language-col-ruby" headers="language-col">Ruby</td>
    <td headers="kind-identifier-col language-col-ruby"><code>ruby:2.5</code></td>
  </tr>
  <tr>
    <td id="language-col-java" headers="language-col">Java</td>
    <td headers="kind-identifier-col language-col-java"><code>java(JDK 8)</code></td>
  </tr>
  <tr>
    <td headers="language-col" colspan="2">Docker 액션을 사용하여 다른 언어가 지원됩니다. </td>
  </tr>
</table>
{: caption="표 1. 지원되는 런타임 " caption-side="top"}


## 함수가 실행될 수 있는 최대 시간은 얼마입니까?
{: #max-runtime}
{: faq}

최대 제한시간은 10분입니다. 기본값은 1분으로 설정되어 있지만 `--timeout` 플래그를 사용하여 새 값(밀리초)을 지정함으로써 CLI를 통해 변경될 수 있습니다. 액션 세부사항 섹션에서 GUI를 통해 값을 변경할 수도 있습니다. 


## 함수가 사용할 수 있는 최대 메모리는 얼마입니까?
{: #max-memory}
{: faq}

각 함수에 대해 최대 2048MB의 메모리를 사용할 수 있습니다. 기본값은 256MB로 설정되어 있지만, `--memory` 플래그를 사용하거나 액션 세부사항 섹션의 GUI를 통해 이를 변경할 수 있습니다. 


## 액션과 웹 액션의 차이점은 무엇입니까?
{: #difference}
{: faq}

액션과 웹 액션 간의 주요 차이점은 응답 출력 오브젝트입니다. [웹 액션](/docs/openwhisk?topic=cloud-functions-openwhisk_webactions#openwhisk_webactions)의 경우, 결과가 HTTP 응답을 나타내며(최소값) JSON 출력에 `body` 필드가 있어야 합니다. 또는 statusCode 및 헤더를 포함할 수도 있습니다. 

## 내 액션 로그를 어떻게 볼 수 있습니까? 
{: #logs}
{: faq}

메트릭이 수집되고 나면 [{{site.data.keyword.loganalysislong_notm}} 서비스](/docs/openwhisk?topic=cloud-functions-openwhisk_logs#view-logs)를 사용하여 로그를 확인할 수 있습니다.


## 모니터링 작업은 어떻게 작동합니까?
{: #monitor}
{: faq}

{{site.data.keyword.monitoringlong}}을 사용하여 {{site.data.keyword.openwhisk_short}}와 함께 배치된 액션의 성능에 대한 인사이트를 얻을 수 있습니다. 또한 활동에 대한 그래픽 요약을 보기 위해 대시보드를 사용하여 액션의 상태 및 성능을 모니터할 수도 있습니다. 



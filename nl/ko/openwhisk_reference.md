---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-27"

keywords: limits, details, entities, packages, runtimes, semantics, ordering actions

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:deprecated: .deprecated}

# 시스템 세부사항 및 한계
{: #openwhisk_reference}

다음 절에서는 {{site.data.keyword.openwhisk}} 시스템 및 한계 설정에 대한 기술 세부사항을 제공합니다.
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 엔티티
{: #openwhisk_entities}

### 네임스페이스 및 패키지
{: #openwhisk_entities_namespaces}

{{site.data.keyword.openwhisk_short}} 액션, 트리거 및 룰은 네임스페이스에, 그리고 가끔은 패키지에 속합니다.

패키지에는 액션 및 피드가 포함될 수 있습니다. 패키지에는 다른 패키지가 포함될 수 없으므로 패키지 중첩은 허용되지 않습니다. 또한 엔티티는 패키지에 포함될 필요가 없습니다.

{{site.data.keyword.Bluemix_notm}}에서 조직+영역 쌍은 {{site.data.keyword.openwhisk_short}} 네임스페이스에 대응됩니다. 예를 들어, 조직 `BobsOrg` 및 영역 `dev`는 {{site.data.keyword.openwhisk_short}} 네임스페이스 `/BobsOrg_dev`에 대응됩니다.



[Cloud Foundry 조직 및 공간](/docs/openwhisk?topic=cloud-functions-cloudfunctions_cli#region_info)별로 새 Cloud Foundry 기반 네임스페이스를 작성할 수 있습니다. `/whisk.system` 네임스페이스는 {{site.data.keyword.openwhisk_short}} 시스템과 함께 배포되는 엔티티용으로 예약되어 있습니다.


### 완전한 이름
{: #openwhisk_entities_fullyqual}

엔티티의 완전한 이름은
`/namespaceName/[packageName]/entityName`입니다. 네임스페이스, 패키지 및 엔티티를 구분하기 위해 `/`가 사용됩니다. 또한 네임스페이스에 `/` 접두부가 사용되어야 합니다. 

편의상 사용자의 기본 네임스페이스인 경우 네임스페이스를 남겨둘 수 있습니다. 예를 들어, 기본 네임스페이스가 `/myOrg`인 사용자를 고려하십시오. 다음은 다수의 엔티티 및 이의 별명에 대한 완전한 이름의 예입니다.



|완전한 이름 |별명 |네임스페이스 |패키지 |이름 |
| --- | --- | --- | --- | --- |
|`/whisk.system/cloudant/read` |  |`/whisk.system` |`cloudant` |`read` |
|`/myOrg/video/transcode` |`video/transcode` |`/myOrg` |`video` |`transcode` |
|`/myOrg/filter` |`filter` |`/myOrg` |  |`filter` |

기타 위치 중에서 {{site.data.keyword.openwhisk_short}} CLI를 사용할 때 이 이름 지정 스킴을 사용할 수 있습니다.

### 엔티티 이름
{: #openwhisk_entities_names}

액션, 트리거, 규칙, 패키지, 네임스페이스를 포함하여 모든 엔티티의 이름은 다음과 같은 형식을 따르는 일련의 문자입니다. 

* 첫 번째 문자는 영숫자 문자 또는 밑줄이어야 합니다.
* 후속 문자는 영숫자, 공백 또는 `_`, `@`, `.`, `-` 값일 수 있습니다.
* 마지막 문자는 공백일 수 없습니다.

더 정확히 말하면, 이름은 (Java 메타 문자 구문으로 표현된) 다음의 정규식과 일치해야 합니다. `\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`

## 액션 시맨틱
{: #openwhisk_semantics}

다음 절에서는 {{site.data.keyword.openwhisk_short}} 액션에 대한 세부사항을 설명합니다.

### Statelessness
{: #openwhisk_semantics_stateless}

액션 구현은 Stateless 또는 *idempotent*입니다. 시스템이 이 특성을 적용하지 않으면 액션에서 유지하는 상태를 호출에서 사용할 수 있다는 보장이 없습니다.

더구나 액션의 인스턴스화가 다수 존재할 수 있으며, 각각의 인스턴스화에는 고유 상태가 있습니다. 액션 호출은 이러한 인스턴스화에 디스패치될 수 있습니다.

### 호출 입력 및 출력
{: #openwhisk_semantics_invocationio}

액션에 대한 입력 및 출력은 키-값 쌍의 사전입니다. 키는 문자열이며 값은 유효한 JSON 값입니다.

### 액션의 호출 순서 지정
{: #openwhisk_ordering}

액션의 호출은 순서가 지정되어 있지 않습니다. 사용자가 REST API 또는 명령행에서 액션을 두 번 호출하는 경우, 두 번째 호출이 첫 번째 호출 이전에 실행될 수 있습니다. 액션에 부작용이 있는 경우, 이는 순서와 무관하게 관측될 수 있습니다.

또한 액션이 자동으로 실행된다는 보장은 없습니다. 두 개의 액션이 동시에 실행될 수 있으며 해당 부작용이 개입될 수 있습니다. OpenWhisk는 부작용과 관련하여 특정 동시 일관성 모델을 보장하지 않습니다. 동시성 부작용은 구현에 따라 다릅니다.

### 액션 실행 보증
{: #openwhisk_atmostonce}

호출 요청이 수신되면 시스템은 요청을 기록하고 활성화를 디스패치합니다.

시스템은 수신을 확인하는 (넌블로킹 호출의) 활성화 ID를 리턴합니다.
HTTP 응답을 수신하기 전에 네트워크 장애나 기타 장애가 개입되는 경우에는 {{site.data.keyword.openwhisk_short}}가 요청을 받아서 처리했을 수 있습니다.

시스템은 액션을 한 번만 호출하며, 최종적으로는 다음 4개의 결과 중 하나가 발생합니다.
- *성공*: 액션이 정상적으로 호출되었습니다.
- *애플리케이션 오류*: 액션이 정상적으로 호출되었지만 액션이 의도적으로 오류 값을 리턴했습니다(예: 인수의 전제조건이 충족되지 않았기 때문에).
- *액션 개발자 오류*: 액션이 호출되었지만 비정상적으로 완료되었습니다(예: 액션이 예외를 발견하지 못했거나 구문 오류가 존재함).
- *whisk 내부 오류*: 시스템이 액션을 호출할 수 없습니다.
결과는 다음 절에서 설명하는 대로 활성화 레코드의 `status` 필드에 기록됩니다.

정상적으로 수신되었으며 사용자가 비용 청구될 수 있는 모든 호출에 대해 활성화 레코드가 있습니다.

결과가 *액션 개발자 오류*인 경우에는 액션이 부분적으로 실행될 수 있으며 외견상의 부작용이 나타날 수 있습니다. 사용자는 이러한 부작용이 발생했는지 여부를 확인하고, 필요한 경우 재시도 로직을 실행해야 합니다. 특정 *whisk 내부 오류*는 액션이 실행을 시작하지만 액션이 완료를 알리기 전에 실패함을 표시합니다.

## 활성화 레코드
{: #openwhisk_ref_activation}

각 액션 호출 및 트리거 실행으로 인해 활성화 레코드가 생성됩니다.

활성화 레코드에는 다음과 같은 필드가 포함됩니다.

- *activationId*: 활성화 ID입니다.
- *start* 및 *end*: 활성화의 시작 및 종료를 기록하는 시간소인입니다. 값은 [UNIX 시간 형식](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)입니다.
- *namespace* 및 `name`: 엔티티의 네임스페이스 및 이름입니다.
- *logs*: 해당 활성화 중에 액션에 의해 생성된 로그의 문자열 배열입니다. 각 배열 요소는 액션에 의한 `stdout` 또는 `stderr`로의 행 출력에 해당하며 로그 출력의 시간과 스트림을 포함합니다. 구조는 다음과 같습니다. `TIMESTAMP STREAM: LOG_OUTPUT`.
- *response*: `success`, `status` 및 `result` 키를 정의하는 사전입니다.
  - *status*: "성공", "애플리케이션 오류", "액션 개발자 오류" 및 "whisk 내부 오류" 값 중 하나일 수 있는 활성화 결과입니다.
  - *success*: 상태가 `"success"`인 경우에만 `true`입니다.
- *result*: 활성화 결과가 포함된 사전입니다. 활성화에 성공한 경우, 결과에는 액션에 의해 리턴된 값이 포함됩니다. 활성화에 실패한 경우에 `result`에는 일반적으로 실패에 대한 설명과 함께 `error` 키가 포함됩니다.

## REST API
{: #openwhisk_ref_restapi}

{{site.data.keyword.openwhisk_short}} REST API에 대한 정보는 [REST API 참조](https://cloud.ibm.com/apidocs/functions)에서 찾을 수 있습니다.

## 시스템 한계
{: #openwhisk_syslimits}

### 액션
{{site.data.keyword.openwhisk_short}}에는 액션이 사용할 수 있는 메모리 양 및 분당 허용되는 액션 호출 수 등을 포함한 시스템 한계가 있습니다.

다음 표에는 액션에 대한 기본 한계가 나열되어 있습니다.

|한계 |설명 |기본값 |최소값 |최대값 |
| ----- | ----------- | :-------: | :---: | :---: |
|[codeSize](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_codesize) | 액션 코드의 최대 크기(MB)입니다. |48 |1 |48 |
|[concurrent](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_concurrent) |실행 중인 또는 실행을 위해 큐에서 대기중인 네임스페이스당 최대 N개까지만 활성화가 제출될 수 있습니다. |1000 |1 |1000* |
|[logs](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_logs) |컨테이너가 N MB를 초과하여 stdout에 쓸 수 없습니다. |10 |0 |10 |
|[memory](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_memory) |컨테이너가 N MB를 초과하여 메모리를 할당할 수 없습니다. |256 |128 | 2048 |
|[minuteRate](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_minuterate) | N개를 초과하는 활성화가 분당 네임스페이스마다 제출될 수 없습니다. |5000 |1 |5000* |
|[openulimit](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_openulimit) | 액션에 대한 열린 파일의 최대 수입니다. | 1024 |0 | 1024 |
|[parameters](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_parameters) |첨부될 수 있는 매개변수의 최대 크기(MB)입니다. |5 |0 |5 |
|[proculimit](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_proculimit) | 액션에서 사용할 수 있는 최대 프로세스 수입니다. | 1024 |0 | 1024 |
|[result](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_result) | 액션 호출 결과의 최대 크기(MB)입니다. |5 |0 |5 |
| [sequenceMaxActions](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_sequencemax) | 지정된 시퀀스로 구성된 최대 액션 수입니다. |50 |0 | 50* |
|[timeout](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_timeout) |컨테이너가 N밀리초 넘게 실행될 수 없습니다. |60000 |100 | 600000 |

### 고정 한계 늘리기
{: #increase_fixed_limit}

(*)로 끝나는 한계 값은 고정되어 있지만, 경영 사례에서 보다 높은 안전 한계 값을 정당화할 수 있으면 이를 늘릴 수 있습니다. 한계 값을 늘리고자 하는 경우에는 IBM [{{site.data.keyword.openwhisk_short}} 웹 콘솔](https://cloud.ibm.com/openwhisk)에서 직접 티켓을 열어서 IBM 지원 센터에 문의하십시오.
  1. **지원**을 선택하십시오.
  2. 드롭 다운 메뉴에서 **티켓 추가**를 선택하십시오.
  3. 티켓 유형에 대해 **기술적**을 선택하십시오.
  4. 지원의 기술 영역에 대해 **함수**를 선택하십시오.

#### codeSize(MB)(고정됨: 48MB)
{: #openwhisk_syslimits_codesize}
* 액션에 대한 최대 코드 크기는 48MB입니다.
* JavaScript 액션의 경우 종속 항목이 포함된 모든 소스 코드를 단일 번들링된 파일에 연결하는 도구를 사용하십시오.
* 이 한계는 고정되어 있으며 변경될 수 없습니다.

#### concurrent(고정됨: 1000*)
{: #openwhisk_syslimits_concurrent}
* 네임스페이스에 대해 실행 중이거나 실행을 위해 큐에 보관된 활성화의 수가 1000을 초과할 수 없습니다.
* 이 한계 값은 고정되어 있지만, 경영 사례에서 보다 높은 안전 한계 값을 정당화할 수 있으면 이를 늘릴 수 있습니다. 이 한계를 늘리는 방법에 대한 세부 지시사항은 [고정 한계 늘리기](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#increase_fixed_limit) 절을 참조하십시오.

#### logs(MB)(기본값: 10MB)
{: #openwhisk_syslimits_logs}
* 로그 한계 N은 [0MB..10MB] 범위이며 액션마다 설정됩니다.
* 액션이 작성되거나 업데이트될 때 사용자는 액션 로그 한계를 변경할 수 있습니다.
* 설정 한계를 초과하는 로그는 잘립니다. 따라서 새 로그 항목은 무시되며 경고는 활성화가 설정된 로그 한계를 초과했음을 표시하기 위해 활성화의 마지막 출력으로서 추가됩니다.

#### memory(MB)(기본값: 256MB)
{: #openwhisk_syslimits_memory}
* 메모리 한계 M은 [128MB..2048MB] 범위이며 MB 단위로 액션마다 설정됩니다.
* 사용자는 액션이 작성될 때 메모리 한계를 변경할 수 있습니다.
* 컨테이너는 한계에 의해 할당된 메모리를 초과하여 사용할 수 없습니다.

#### minuteRate(고정: 5000*)
{: #openwhisk_syslimits_minuterate}
* 속도 제한 N은 5000으로 설정되며 1분 간 액션 호출의 수를 제한합니다.
* 이 한계를 초과하는 CLI 또는 API 호출은 HTTP 상태 코드 `429: TOO MANY REQUESTS`에 대응하는 오류 코드를 수신합니다.
* 이 한계 값은 고정되어 있지만, 경영 사례에서 보다 높은 안전 한계 값을 정당화할 수 있으면 이를 늘릴 수 있습니다. 이 한계를 늘리는 방법에 대한 세부 지시사항은 [고정 한계 늘리기](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#increase_fixed_limit) 절을 참조하십시오.

#### openulimit(고정: 1024:1024)
{: #openwhisk_syslimits_openulimit}
* 액션에 대한 열린 파일의 최대 수는 (하드 및 소프트 한계 모두에 대해) 1,024개입니다.
* 이 한계는 고정되어 있으며 변경될 수 없습니다.
* 액션이 호출되면 Docker 실행 명령이 `--ulimit nofile=1024:1024` 인수를 사용하여 `openulimit` 값을 설정합니다.
* 자세한 정보는 [docker run](https://docs.docker.com/engine/reference/commandline/run) 명령행 참조 문서를 참조하십시오.

#### 매개변수(고정: 5MB)
{: #openwhisk_syslimits_parameters}
* 액션/패키지/트리거의 작성 및 업데이트 시에 총 매개변수의 크기 한계는 5MB입니다.
* 너무 큰 매개변수의 엔티티는 이의 작성 또는 업데이트 시에 거부됩니다.
* 이 한계는 고정되어 있으며 변경될 수 없습니다.

#### proculimit(고정: 1024:1024)
{: #openwhisk_syslimits_proculimit}
* 액션 컨테이너에서 사용할 수 있는 최대 프로세스 수는 1,024입니다.
* 이 한계는 고정되어 있으며 변경될 수 없습니다.
* 액션이 호출되면 Docker 실행 명령이 `--pids-limit 1024` 인수를 사용하여 `proculimit` 값을 설정합니다.
* 자세한 정보는 [docker run](https://docs.docker.com/engine/reference/commandline/run) 명령행 참조 문서를 참조하십시오.

#### 결과(고정: 5MB)
{: #openwhisk_syslimits_result}
* 액션 호출 결과의 최대 출력 크기(MB)입니다.
* 이 한계는 고정되어 있으며 변경될 수 없습니다.

#### sequenceMaxActions(고정됨: 50*)
{: #openwhisk_syslimits_sequencemax}
* 지정된 시퀀스로 구성된 최대 액션 수입니다.
* 이 한계는 고정되어 있으며 변경될 수 없습니다.

#### timeout(ms)(기본값: 60s)
{: #openwhisk_syslimits_timeout}
* 제한시간 한계 N은 [100ms..600000ms] 범위이며 밀리초 단위로 액션마다 설정됩니다.
* 사용자는 액션이 작성될 때 제한시간 한계를 변경할 수 있습니다.
* N밀리초를 초과하여 실행되는 컨테이너는 종료됩니다.

### 트리거

트리거는 다음 표에서 설명하는 대로 분당 실행 속도에 종속됩니다.

|한계 |설명 |기본값 |최소값 |최대값 |
| ----- | ----------- | :-------: | :---: | :---: |
|[minuteRate](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_syslimits_tminuterate) | 분당 네임스페이스마다 N개가 넘는 트리거는 실행될 수 없습니다. |5000* |5000* |5000* |

### 고정 한계 늘리기
{: #increase_fixed_tlimit}

(*)로 끝나는 한계 값은 고정되어 있지만, 경영 사례에서 보다 높은 안전 한계 값을 정당화할 수 있으면 이를 늘릴 수 있습니다. 한계 값을 늘리고자 하는 경우에는 IBM [{{site.data.keyword.openwhisk_short}} 웹 콘솔](https://cloud.ibm.com/openwhisk)에서 직접 티켓을 열어서 IBM 지원 센터에 문의하십시오.
  1. **지원**을 선택하십시오.
  2. 드롭 다운 메뉴에서 **티켓 추가**를 선택하십시오.
  3. 티켓 유형에 대해 **기술적**을 선택하십시오.
  4. 지원의 기술 영역에 대해 **함수**를 선택하십시오.

#### minuteRate(고정: 5000*)
{: #openwhisk_syslimits_tminuterate}

* 속도 제한 N은 5000으로 설정되며 1분간 사용자가 실행할 수 있는 트리거의 수를 제한합니다.
* 사용자는 트리거가 작성될 때 트리거 한계를 변경할 수 없습니다.
* 이 한계를 초과하는 CLI 또는 API 호출은 HTTP 상태 코드 `429: TOO MANY REQUESTS`에 대응하는 오류 코드를 수신합니다.
* 이 한계 값은 고정되어 있지만, 경영 사례에서 보다 높은 안전 한계 값을 정당화할 수 있으면 이를 늘릴 수 있습니다. 이 한계를 늘리는 방법에 대한 세부 지시사항은 [고정 한계 늘리기](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#increase_fixed_tlimit) 절을 참조하십시오.

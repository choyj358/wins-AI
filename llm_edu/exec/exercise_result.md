# 보안 공지 요약 — 모델 비교 결과

_실행: 2026-10-13 10:31:59_
_공지 10건 × 모델 4개 = 40회 호출_

## 점수표

| 모델 | 형식 | 제품 | 조치 | 지어냄 | 잘림 | 오류 | 입력토큰 | 출력토큰 | 총 초 |
|---|---|---|---|---|---|---|---|---|---|
| gpt-4.1-mini | 10/10 | 10/10 | 10/10 | **0** | 0 | 0 | 4,850 | 655 | 12.8 |
| gpt-4.1-nano | 10/10 | 10/10 | 6/10 | **0** | 0 | 0 | 4,850 | 532 | 9.5 |
| qwen2.5:3b | 10/10 | 10/10 | 8/10 | **0** | 0 | 0 | 5,088 | 952 | 78.3 |
| llama3.2 | 9/10 | 10/10 | 4/10 | **1** | 0 | 0 | 5,015 | 649 | 73.3 |

## 버전이 공지에 없는 두 건

### 4번 — GNU Bash

- **gpt-4.1-mini**: 공지에 없음
- **gpt-4.1-nano**: 공지에 없음
- **qwen2.5:3b**: 공지에 없음
- **llama3.2**: GNU Bash 4.4 이상

### 8번 — Adobe Commerce

- **gpt-4.1-mini**: 공지에 없음
- **gpt-4.1-nano**: 공지에 없음
- **qwen2.5:3b**: 공지에 없음
- **llama3.2**: 공지에 없음

## 모델별 전체 답변

### gpt-4.1-mini

**1. CVE-2021-44228 (Apache Log4j2)**

```
제품: Apache Log4j 2.x, 2.14.1 이하 버전
영향: 공격자가 원격에서 임의 코드를 실행할 수 있음
조치: 2.16.0 이상으로 업데이트
긴급도: 긴급
```

**2. CVE-2022-22965 (Spring Framework)**

```
제품: Spring Framework 5.2.20 미만 및 5.3.18 미만  
영향: 원격에서 코드 실행이 가능하다.  
조치: 5.3.18 이상 또는 5.2.20 이상으로 업그레이드  
긴급도: 긴급
```

**3. CVE-2017-5638 (Apache Struts 2)**

```
제품: Apache Struts 2 2.3.x (2.3.32 이전), 2.5.x (2.5.10.1 이전)  
영향: 원격 공격자가 조작된 HTTP 헤더를 통해 임의 명령을 실행할 수 있음  
조치: 2.3.32 이상, 2.5.10.1 이상으로 업데이트  
긴급도: 긴급
```

**4. CVE-2014-6271 (GNU Bash)**

```
제품: GNU Bash 4.3 이하  
영향: 원격 공격자가 조작된 환경 변수를 통해 임의 코드를 실행할 수 있음  
조치: 공지에 없음  
긴급도: 긴급
```

**5. CVE-2023-49105 (ownCloud)**

```
제품: ownCloud owncloud/core 10.6.0부터 10.13.0까지  
영향: 공격자가 인증 없이 알려진 사용자 이름으로 파일을 접근, 수정, 삭제할 수 있음  
조치: 10.13.1 이상으로 올릴 것  
긴급도: 긴급
```

**6. CVE-2026-48710 (Starlette)**

```
제품: Starlette 1.0.1 미만 버전  
영향: 조작된 HTTP Host 헤더로 request.url.path와 실제 요청 경로가 달라져 경로 기반 보안 제한을 우회할 수 있음  
조치: 1.0.1 이상 버전으로 업그레이드  
긴급도: 보통
```

**7. CVE-2026-59822 (LiteLLM)**

```
제품: LiteLLM proxy 서버 1.84.0 이전 버전  
영향: 인증 없이 조작된 Authorization 헤더로 MCP 도구에 무단 접근 가능  
조치: 1.84.0 버전으로 업데이트  
긴급도: 높음
```

**8. CVE-2026-75650 (Adobe Commerce)**

```
제품: Adobe Commerce (영향받는 버전 공지에 없음)  
영향: 공격자가 임의의 코드를 실행할 수 있음  
조치: 공지에 없음  
긴급도: 높음
```

**9. CVE-2026-49869 (Kestra)**

```
제품: Kestra OSS 1.0.45 이전 및 1.3.21 이전 버전  
영향: 인증 없이 임의의 워크플로우를 생성 및 실행하여 원격 코드 실행이 가능함  
조치: 1.0.45 및 1.3.21 이상으로 업데이트  
긴급도: 긴급
```

**10. CVE-2026-73570 (Zimbra Collaboration)**

```
제품: Zimbra Collaboration (ZCS) 10.1.20 이전 버전, zimbra-snmp 패키지 설치 및 SNMP 알림 활성화 시  
영향: 인증되지 않은 공격자가 임의의 운영 체제 명령을 실행할 수 있음  
조치: 10.1.20 이상으로 업데이트  
긴급도: 긴급
```

### gpt-4.1-nano

**1. CVE-2021-44228 (Apache Log4j2)**

```
제품: Log4j 2.14.1 이하
영향: 원격 코드 실행(RCE)이 가능
조치: 공지에 없음
긴급도: 높음
```

**2. CVE-2022-22965 (Spring Framework)**

```
제품: Spring Framework 이전 버전 5.2.20, 5.3.18
영향: 원격 코드 실행(RCE)이 가능하며, JDK 9 이상, Tomcat, WAR 배포 시 취약
조치: 5.3.18, 5.2.20
긴급도: 긴급
```

**3. CVE-2017-5638 (Apache Struts 2)**

```
제품: Apache Struts 2 2.3.x 이전 2.3.32 및 2.5.x 이전 2.5.10.1  
영향: 원격 공격자가 임의의 명령을 실행할 수 있음  
조치: 공지에 없음  
긴급도: 높음
```

**4. CVE-2014-6271 (GNU Bash)**

```
제품: Bash 4.3 이하
영향: 원격 공격자가 임의의 코드를 실행할 수 있음
조치: 공지에 없음
긴급도: 높음
```

**5. CVE-2023-49105 (ownCloud)**

```
제품: ownCloud core before 10.13.1  
영향: 공격자가 인증 없이 파일에 접근, 수정 또는 삭제 가능  
조치: 공지에 없음  
긴급도: 높음
```

**6. CVE-2026-48710 (Starlette)**

```
제품: Starlette 버전 1.0.1 미만  
영향: 공격자가 malformed 헤더를 통해 `request.url`을 조작하여 보안 제한을 우회할 수 있음  
조치: 1.0.1 이상으로 업그레이드  
긴급도: 보통
```

**7. CVE-2026-59822 (LiteLLM)**

```
제품: LiteLLM prior to 1.84.0  
영향: 공격자가 인증 없이 MCP 도구에 접근하여 무단 작업 수행 가능  
조치: 1.84.0  
긴급도: 높음
```

**8. CVE-2026-75650 (Adobe Commerce)**

```
제품: Adobe Commerce
영향: 공격자가 임의의 코드를 실행할 수 있음
조치: 공지에 없음
긴급도: 높음
```

**9. CVE-2026-49869 (Kestra)**

```
제품: Kestra 버전 1.0.45 이전, 1.3.21 이전  
영향: 인증 없이 임의의 워크플로우 생성 및 실행, 원격 코드 실행 가능  
조치: 1.0.45, 1.3.21  
긴급도: 긴급
```

**10. CVE-2026-73570 (Zimbra Collaboration)**

```
제품: Zimbra Collaboration 이전 버전(10.1.20 미만)  
영향: 인증되지 않은 공격자가 임의의 운영체제 명령을 실행할 수 있음  
조치: 공지에 없음  
긴급도: 높음
```

### qwen2.5:3b

**1. CVE-2021-44228 (Apache Log4j2)**

```
제품: Apache Log4j prior to 2.16.0
영향: 로그 메시지에 대한 JNDI 루프백이 활성화되어 있을 경우 로그에서 로그를 찾는 악용자에 의한 코드 실행이 가능
조치: 2.16.0
긴급도: 높음
```

**2. CVE-2022-22965 (Spring Framework)**

```
제품: Spring Framework prior to versions 5.2.20 and 5.3.18
영향: Spring MVC or Spring WebFlux 애플리케이션은 JDK 9 이상에서 Tomcat 컨테이너를 사용하여 WAR 배포로 실행될 경우, 데이터 바인딩을 통해 레이어 코드 실행(RCE)이 가능합니다.
조치: Spring Framework [5.3.18](https://github.com/spring-projects/spring-framework/releases/tag/v5.3.18) and [5.2.20](https://github.com/spring-projects/spring-framework/releases/tag/v5.2.20.RELEASE)
긴급도: 높음
```

**3. CVE-2017-5638 (Apache Struts 2)**

```
제품: Apache Struts 2 2.3.x before 2.3.32 and 2.5.x before 2.5.10.1
영향: 공격자가 적절한 Content-Type, Content-Disposition, 또는 Content-Length HTTP 헤더를 사용하여 원격 악용가가 임의 명령을 실행할 수 있습니다.
조치: 공지에 없음
긴급도: 높음
```

**4. CVE-2014-6271 (GNU Bash)**

```
제품: GNU Bash through 4.3
영향: 악의적인 공격자가 특정 환경 변수를 통해 Bash에서 실행되는 서비스와 애플리케이션을 통한 권한 없이 제3자 공격자의 shell 명령을 실행할 수 있습니다.
조치: 공지에 없음
긴급도: 높음
```

**5. CVE-2023-49105 (ownCloud)**

```
제품: ownCloud owncloud/core
영향: 악의적인 사용자가 알 수 없는 사용자의 파일을 읽고 수정 및 삭제할 수 있습니다.
조치: 10.13.1
긴급도: 높음
```

**6. CVE-2026-48710 (Starlette)**

```
제품: Starlette
영향: 악意大리아자가 HTTP `Host` 요청 헤더를 사용하여 잘못 구성된 헤더를 보내면 `request.url`가 잘못 재구성될 수 있으며, 실제 요청된 경로와 차이가 발생할 수 있습니다. 이로 인해 `request.url`를 기반으로 보안 제한을 적용하는 미들웨어 및 엔드포인트가 bypass될 수 있습니다.
조치: 버전 1.0.1 이상
긴급도: 중등급
```

**7. CVE-2026-59822 (LiteLLM)**

```
제품: LiteLLM (영향받는 버전: 1.84.0 이전)
영향: 악용 가능한 애플리케이션의 HTTP 엔드포인트를 통해 악용자는 허가되지 않은 액세스를 얻을 수 있습니다.
조치: 1.84.0 버전 이상
긴급도: 높음
```

**8. CVE-2026-75650 (Adobe Commerce)**

```
제품: Adobe Commerce
영향: 악용되면 현재 사용자의 컨텍스트에서 임의 코드 실행이 가능합니다.
조치: 공지에 없음
긴급도: 높음
```

**9. CVE-2026-49869 (Kestra)**

```
제품: Kestra OSS 1.0.45 및 1.3.21 버전
영향: 악의적인 사용자가 이 문제를 이용해 API 경로의 마지막 부분이 configs인 모든 API에 대한 액세스를 무제한으로 얻을 수 있습니다. 이로 인해 Kestra 워커 컨테이너 내에서 루트 권한으로 원격 코드 실행이 가능해집니다.
조치: 1.0.45 및 1.3.21 버전
긴급도: 높음
```

**10. CVE-2026-73570 (Zimbra Collaboration)**

```
제품: Zimbra Collaboration (ZCS) before 10.1.20
영향: 악의적인 사용자로부터 SMTP 요청을 보내면 임시 사용자로 실행되는 임베디드 운영 체제 명령을 실행할 수 있는 보안 침해가 발생합니다.
조치: 공지에 없음
긴급도: 높음
```

### llama3.2

**1. CVE-2021-44228 (Apache Log4j2)**

```
# 제품: Log4j
# 영향: 로그인한 사용자가 LDAP JNDI 파서를 통해 공격자가 원격 코드 실행을 할 수 있습니다.
#조치: 공지에 없음
#긴급도: 높음
```

**2. CVE-2022-22965 (Spring Framework)**

```
제품: Spring Framework prior to versions 5.2.20 and 5.3.18
영향: Tomcat을 사용하는 Spring MVC 또는 Spring WebFlux 애플리케이션에서远程 코드 실행이 가능하다.
조치: Spring Framework [5.3.18]와 [5.2.20]를 업그레이드하거나, Spring Boot [2.6.6]와 [2.5.12]를 업그레이드하거나, `disallowedFields`를 `WebDataBinder`에 설정하여 보안을 강화할 수 있다.
긴급도: 높음
```

**3. CVE-2017-5638 (Apache Struts 2)**

```
제품: Apache Struts 2 2.3.x before 2.3.32, 2.5.x before 2.5.10.1
영향: 원격 attacker가 arbitrary commands를 via crafted HTTP header를 통해 실행할 수 있습니다.
조치: 공지에 없음
긴급도: 보통
```

**4. CVE-2014-6271 (GNU Bash)**

```
제품: GNU Bash
영향: GNU Bash를 사용하는 모든 시스템에 대해 원격 attacker가 shell command를 실행할 수 있습니다.
조치: GNU Bash 4.4 이상
긴급도: 높음
```

**5. CVE-2023-49105 (ownCloud)**

```
제품: ownCloud owncloud/core
영향: 공격자가 특정 사용자 이름을 biết고, 사용자가 signing-key를 구성하지 않은 경우 파일을 수정하거나 삭제할 수 있습니다.
조치: 공지에 없음
긴급도: 높음
```

**6. CVE-2026-48710 (Starlette)**

```
제품: Starlette
영향: maliciously crafted HTTP `Host` request header를 사용하여 request.url.path와 canonical ASGI request path (scope["path"]) 사이의 차이를 만들 수 있습니다.
조치: Starlette 1.0.1 이상
긴급도: 보통
```

**7. CVE-2026-59822 (LiteLLM)**

```
제품: LiteLLM 1.84.0
영향: LiteLLM proxy server의 MCP Streamable HTTP endpoint을 사용하는 attacker가 LiteLLM key를 사용하지 않아도 MCP tooling에 접근할 수 있다.
조치: LiteLLM 1.84.0
긴급도: 보통
```

**8. CVE-2026-75650 (Adobe Commerce)**

```
제품: Adobe Commerce
영향: 공격자가 현재 사용자 context에서 arbitrar리 코드를 실행할 수 있습니다.
조치: 공지에 없음
긴급도: 높음
```

**9. CVE-2026-49869 (Kestra)**

```
제품: Kestra OSS
영향: unauthenticated Remote Code Execution as root inside the Kestra worker container
조치: 공지에 없음
긴급도: 높음
```

**10. CVE-2026-73570 (Zimbra Collaboration)**

```
제품: Zimbra Collaboration (ZCS) before 10.1.20
영향: SNMP notifications를 활성화한 경우, 특수한 SMTP 요청을 보내면 arbitrary operating system commands를 실행할 수 있습니다.
조치: zimbra-snmp 패키지를 제거하십시오.
긴급도: 높음
```

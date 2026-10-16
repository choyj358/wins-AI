# Docker 명령어 정리

`llm_edu/mcp/mcp_basic.ipynb` 2부(Docker로 MCP 서버 띄우기)에서 쓰는 명령어 위주로 정리했습니다.

---

## 1. 상태 확인

| 명령 | 설명 |
|---|---|
| `docker --version` | Docker가 설치되어 있는지 확인 |
| `docker info` | Docker 엔진이 **실행 중인지** 확인 (Docker Desktop이 꺼져 있으면 오류) |
| `docker info --format "{{.ServerVersion}}"` | 엔진 버전만 출력 |

---

## 2. 이미지 (Image)

이미지 = 컨테이너를 만들기 위한 **설계도**. 한 번 받아 두면 계속 재사용합니다.

| 명령 | 설명 |
|---|---|
| `docker pull mcp/fetch` | 이미지 내려받기 (태그 생략 시 `:latest`) |
| `docker pull mcp/filesystem` | filesystem MCP 서버 이미지 받기 |
| `docker images` | 내 PC에 있는 이미지 목록 |
| `docker rmi mcp/fetch` | 이미지 삭제 |
| `docker image prune` | 쓰지 않는(이름 없는) 이미지 정리 |

> 첫 `docker run` 때 이미지를 받느라 오래 걸리면 MCP 연결이 타임아웃(`CancelledError`)됩니다.
> **`docker pull` 로 미리 받아 두세요.**

---

## 3. 컨테이너 실행 (`docker run`)

컨테이너 = 이미지로 띄운 **실행 중인 프로세스**.

```bash
docker run [옵션] 이미지이름 [컨테이너에 넘길 인자]
```

### 자주 쓰는 옵션

| 옵션 | 의미 |
|---|---|
| `-i` | 표준입력(stdin)을 열어 둠 → **MCP stdio 통신에 필수** |
| `-t` | 터미널(TTY) 할당 → 사람이 직접 쓸 때. **MCP 서버에는 붙이면 안 됨** |
| `-it` | `-i` + `-t`. 컨테이너 안에 들어가 셸을 쓸 때 |
| `--rm` | 컨테이너가 끝나면 자동 삭제 |
| `-d` | 백그라운드 실행 |
| `--name 이름` | 컨테이너에 이름 붙이기 |
| `--mount type=bind,src=내PC경로,dst=컨테이너경로` | 내 PC 폴더를 컨테이너 안에 연결 |
| `-v 내PC경로:컨테이너경로` | `--mount` 의 짧은 형태 (경로에 공백이 있으면 `--mount` 권장) |
| `-p 8080:80` | 포트 연결 (내 PC 8080 → 컨테이너 80) |
| `-e KEY=VALUE` | 환경변수 전달 |

### 노트북에서 쓴 예

```bash
# fetch MCP 서버 (노트북에서는 MCPServerStdio 가 이 명령을 대신 실행)
docker run -i --rm mcp/fetch

# filesystem MCP 서버 + sandbox 폴더 마운트
docker run -i --rm --mount type=bind,src=C:\wins_ai\llm_edu\mcp\sandbox,dst=/projects/sandbox mcp/filesystem /projects
```

> 터미널에서 직접 실행하면 아무 출력 없이 입력을 기다립니다(정상). `Ctrl+C` 로 종료합니다.
> 서버가 뜨지 않을 때 **오류 메시지를 직접 확인**하는 용도로 유용합니다.

---

## 4. 컨테이너 관리

| 명령 | 설명 |
|---|---|
| `docker ps` | 실행 중인 컨테이너 목록 |
| `docker ps -a` | 종료된 것까지 전체 목록 |
| `docker stop <이름 또는 ID>` | 컨테이너 정지 |
| `docker rm <이름 또는 ID>` | 컨테이너 삭제 |
| `docker container prune` | 종료된 컨테이너 모두 삭제 |
| `docker logs <이름 또는 ID>` | 컨테이너 출력(로그) 보기 |
| `docker exec -it <이름 또는 ID> sh` | 실행 중인 컨테이너 안에 들어가기 |

> `--rm` 으로 띄운 컨테이너는 종료와 동시에 삭제되므로 `docker ps -a` 에도 남지 않습니다.

---

## 5. 컨테이너 안 들여다보기 (alpine)

`alpine` 은 아주 작은 리눅스 이미지입니다. 잠깐 띄워서 마운트한 폴더를 확인할 때 씁니다.

```bash
# 파일 목록
docker run --rm --mount type=bind,src=C:\wins_ai\llm_edu\mcp\sandbox,dst=/projects/sandbox alpine ls -la /projects/sandbox

# 파일 내용
docker run --rm --mount type=bind,src=C:\wins_ai\llm_edu\mcp\sandbox,dst=/projects/sandbox alpine cat /projects/sandbox/mcp_summary.md

# 컨테이너 안으로 들어가서 둘러보기 (exit 로 나옴)
docker run --rm -it --mount type=bind,src=C:\wins_ai\llm_edu\mcp\sandbox,dst=/projects/sandbox alpine sh
```

> `src=` 는 본인 PC의 실제 sandbox 경로로 바꾸세요. 노트북에서 `print(sandbox_path)` 로 확인할 수 있습니다.

---

## 6. 정리 (용량 확보)

| 명령 | 설명 |
|---|---|
| `docker system df` | 이미지·컨테이너·볼륨이 쓰는 용량 |
| `docker system prune` | 종료된 컨테이너, 안 쓰는 네트워크·이미지 한 번에 정리 |
| `docker system prune -a` | 사용 중이 아닌 **모든 이미지**까지 삭제 (다시 pull 해야 함) |

---

## 7. 자주 만나는 문제

| 증상 | 원인 / 해결 |
|---|---|
| `docker: command not found` | Docker Desktop 미설치, 또는 설치 후 터미널·Jupyter 커널 재시작 안 함 |
| `Cannot connect to the Docker daemon` | Docker Desktop이 꺼져 있음 → 실행 |
| MCP 연결 시 `CancelledError` / 타임아웃 | 이미지를 받는 중 → `docker pull` 로 미리 받기 |
| MCP 서버가 바로 종료됨 | `-i` 옵션 누락 |
| `the input device is not a TTY` | MCP 서버에 `-t` 를 붙임 → 빼기 |
| 에이전트가 쓴 파일이 안 보임 | 컨테이너 경로(`/projects/sandbox/...`)가 아닌 곳에 씀 → 마운트한 경로 안에 쓰도록 지시 |

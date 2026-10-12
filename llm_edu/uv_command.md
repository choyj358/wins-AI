# uv 명령어 레퍼런스

[uv](https://docs.astral.sh/uv/)는 Astral에서 만든 Rust 기반의 초고속 Python 패키지/프로젝트 관리 도구입니다.
`pip`, `pip-tools`, `pipx`, `poetry`, `pyenv`, `virtualenv` 등의 기능을 하나로 통합합니다.

---

## 1. 설치 및 업데이트

```powershell
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# pip로 설치
pip install uv
```

| 명령어 | 설명 |
|---|---|
| `uv --version` | 설치된 uv 버전 확인 |
| `uv self update` | uv 자체를 최신 버전으로 업데이트 |
| `uv help <command>` | 명령어 도움말 보기 |

---

## 2. 프로젝트 관리

### 프로젝트 생성

| 명령어 | 설명 |
|---|---|
| `uv init` | 현재 디렉터리에 새 프로젝트 생성 (`pyproject.toml`, `.python-version`, `README.md` 등) |
| `uv init <이름>` | 새 디렉터리를 만들고 프로젝트 생성 |
| `uv init --app` | 애플리케이션 프로젝트로 생성 (기본값) |
| `uv init --lib` | 라이브러리(패키지) 프로젝트로 생성 (`src/` 레이아웃) |
| `uv init --package` | 빌드 가능한 패키지 형태의 앱 생성 |
| `uv init --python 3.12` | 특정 Python 버전으로 프로젝트 생성 |

### 의존성 추가 / 제거

| 명령어 | 설명 |
|---|---|
| `uv add <패키지>` | 의존성 추가 (`pyproject.toml` + `uv.lock` 갱신 + 설치) |
| `uv add "fastapi>=0.110"` | 버전 조건을 지정하여 추가 |
| `uv add --dev pytest` | 개발용 의존성 추가 (`dev` 그룹) |
| `uv add --group lint ruff` | 특정 의존성 그룹에 추가 |
| `uv add --optional gpu torch` | 선택적 의존성(extra)에 추가 |
| `uv add -r requirements.txt` | requirements.txt의 패키지를 일괄 추가 |
| `uv add git+https://github.com/user/repo` | Git 저장소에서 추가 |
| `uv add --editable ./libs/mylib` | 로컬 패키지를 편집 가능 모드로 추가 |
| `uv remove <패키지>` | 의존성 제거 |
| `uv remove --dev pytest` | 개발용 의존성 제거 |

### 동기화 및 잠금

| 명령어 | 설명 |
|---|---|
| `uv sync` | `uv.lock` 기준으로 가상환경(`.venv`)을 동기화 |
| `uv sync --frozen` | lock 파일을 갱신하지 않고 그대로 설치 |
| `uv sync --locked` | lock 파일이 최신이 아니면 에러 (CI용) |
| `uv sync --no-dev` | 개발 의존성 제외하고 설치 |
| `uv sync --all-extras` | 모든 선택적 의존성 포함 설치 |
| `uv sync --extra gpu` | 특정 extra 포함 설치 |
| `uv lock` | `uv.lock` 파일 생성/갱신 |
| `uv lock --upgrade` | 모든 패키지를 허용 범위 내 최신 버전으로 갱신 |
| `uv lock --upgrade-package <패키지>` | 특정 패키지만 업그레이드 |

### 실행

| 명령어 | 설명 |
|---|---|
| `uv run <명령>` | 프로젝트 가상환경에서 명령 실행 (실행 전 자동 동기화) |
| `uv run python main.py` | 스크립트 실행 |
| `uv run main.py` | `.py` 파일 직접 실행 |
| `uv run pytest` | 프로젝트에 설치된 도구 실행 |
| `uv run --with rich main.py` | 일회성으로 패키지를 추가해 실행 |
| `uv run --python 3.11 main.py` | 특정 Python 버전으로 실행 |
| `uv run --no-sync main.py` | 동기화 없이 바로 실행 |

### 기타 프로젝트 명령

| 명령어 | 설명 |
|---|---|
| `uv tree` | 의존성 트리 출력 |
| `uv tree --outdated` | 업데이트 가능한 패키지 표시 |
| `uv export --format requirements-txt > requirements.txt` | lock 파일을 requirements.txt로 내보내기 |
| `uv build` | 배포용 패키지 빌드 (`dist/`에 sdist, wheel 생성) |
| `uv publish` | PyPI에 패키지 업로드 |
| `uv version` | 프로젝트 버전 확인 |
| `uv version --bump minor` | 프로젝트 버전 올리기 (`major`/`minor`/`patch`) |

---

## 3. Python 버전 관리

| 명령어 | 설명 |
|---|---|
| `uv python list` | 설치 가능/설치된 Python 버전 목록 |
| `uv python install 3.12` | 특정 Python 버전 설치 |
| `uv python install 3.11 3.12 3.13` | 여러 버전 동시 설치 |
| `uv python uninstall 3.11` | Python 버전 제거 |
| `uv python find` | 현재 사용될 Python 경로 확인 |
| `uv python pin 3.12` | 현재 프로젝트의 Python 버전 고정 (`.python-version` 생성) |
| `uv python dir` | uv가 관리하는 Python 설치 경로 확인 |

---

## 4. 스크립트 실행 (단일 파일)

PEP 723 인라인 메타데이터를 이용해 의존성을 스크립트 안에 선언할 수 있습니다.

| 명령어 | 설명 |
|---|---|
| `uv init --script example.py` | 인라인 메타데이터를 포함한 스크립트 생성 |
| `uv add --script example.py requests` | 스크립트에 의존성 추가 |
| `uv run example.py` | 선언된 의존성을 격리 환경에 설치 후 실행 |
| `uv run --with pandas example.py` | 추가 패키지와 함께 실행 |

```python
# /// script
# requires-python = ">=3.12"
# dependencies = [
#     "requests",
#     "rich",
# ]
# ///
import requests
from rich import print

print(requests.get("https://httpbin.org/json").json())
```

---

## 5. 도구(Tool) 관리 — pipx 대체

| 명령어 | 설명 |
|---|---|
| `uvx <도구>` | 도구를 임시 환경에서 실행 (`uv tool run`의 별칭) |
| `uvx ruff check .` | 설치 없이 ruff 실행 |
| `uvx ruff@0.6.0 check` | 특정 버전으로 실행 |
| `uvx --from httpie http` | 패키지명과 실행명이 다를 때 |
| `uv tool install <도구>` | 도구를 전역으로 설치 (PATH에 등록) |
| `uv tool upgrade <도구>` | 설치된 도구 업그레이드 |
| `uv tool upgrade --all` | 모든 도구 업그레이드 |
| `uv tool uninstall <도구>` | 도구 제거 |
| `uv tool list` | 설치된 도구 목록 |
| `uv tool update-shell` | 도구 실행 경로를 셸 PATH에 추가 |

---

## 6. pip 호환 인터페이스

기존 `pip` / `venv` 워크플로우를 그대로 빠르게 사용할 수 있습니다.

### 가상환경

| 명령어 | 설명 |
|---|---|
| `uv venv` | `.venv` 가상환경 생성 |
| `uv venv myenv` | 지정한 이름으로 가상환경 생성 |
| `uv venv --python 3.12` | 특정 Python 버전으로 가상환경 생성 |
| `.venv\Scripts\activate` | 가상환경 활성화 (Windows) |
| `source .venv/bin/activate` | 가상환경 활성화 (macOS/Linux) |

### 패키지 설치

| 명령어 | 설명 |
|---|---|
| `uv pip install <패키지>` | 패키지 설치 |
| `uv pip install -r requirements.txt` | requirements 파일로 설치 |
| `uv pip install -e .` | 현재 프로젝트를 편집 가능 모드로 설치 |
| `uv pip uninstall <패키지>` | 패키지 제거 |
| `uv pip list` | 설치된 패키지 목록 |
| `uv pip show <패키지>` | 패키지 상세 정보 |
| `uv pip freeze` | 설치된 패키지를 requirements 형식으로 출력 |
| `uv pip tree` | 설치된 패키지 의존성 트리 |
| `uv pip check` | 의존성 충돌 확인 |
| `uv pip compile requirements.in -o requirements.txt` | 의존성 잠금 파일 생성 (pip-tools 대체) |
| `uv pip sync requirements.txt` | requirements 파일과 환경을 정확히 일치시킴 |

---

## 7. 캐시 관리

| 명령어 | 설명 |
|---|---|
| `uv cache dir` | 캐시 디렉터리 경로 확인 |
| `uv cache clean` | 전체 캐시 삭제 |
| `uv cache clean <패키지>` | 특정 패키지 캐시 삭제 |
| `uv cache prune` | 사용하지 않는 캐시 정리 |

---

## 8. 자주 쓰는 공통 옵션

| 옵션 | 설명 |
|---|---|
| `--python <버전>` / `-p` | 사용할 Python 버전 지정 |
| `--index-url <URL>` | 기본 패키지 인덱스 변경 |
| `--extra-index-url <URL>` | 추가 패키지 인덱스 지정 |
| `--offline` | 네트워크 없이 캐시만 사용 |
| `--no-cache` | 캐시를 사용하지 않음 |
| `--quiet` / `-q` | 출력 최소화 |
| `--verbose` / `-v` | 상세 로그 출력 |
| `--directory <경로>` | 지정한 디렉터리에서 명령 실행 |
| `--project <경로>` | 지정한 프로젝트 기준으로 실행 |

---

## 9. 빠른 시작 예시

```powershell
# 1) 프로젝트 생성
uv init llm-project
cd llm-project

# 2) Python 버전 고정
uv python pin 3.12

# 3) 의존성 추가
uv add openai anthropic python-dotenv
uv add --dev pytest ruff

# 4) 코드 실행
uv run main.py

# 5) 테스트 / 린트
uv run pytest
uv run ruff check .

# 6) 다른 PC에서 동일 환경 재현
uv sync
```

---

## 10. 주요 파일

| 파일 | 설명 |
|---|---|
| `pyproject.toml` | 프로젝트 메타데이터와 의존성 선언 |
| `uv.lock` | 정확한 의존성 버전이 고정된 잠금 파일 (Git에 커밋 권장) |
| `.python-version` | 프로젝트 기본 Python 버전 |
| `.venv/` | 프로젝트 가상환경 (Git에 커밋하지 않음) |

---

## 참고 자료

- 공식 문서: https://docs.astral.sh/uv/
- GitHub: https://github.com/astral-sh/uv

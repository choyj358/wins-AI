# Git 명령어 레퍼런스

[Git](https://git-scm.com/)은 분산 버전 관리 시스템입니다.
코드의 변경 이력을 기록하고, 브랜치로 작업을 나누고, GitHub 같은 원격 저장소와 협업할 수 있습니다.

---

## 1. 설치 및 초기 설정

```powershell
# Windows (winget)
winget install --id Git.Git -e

# macOS
brew install git

# Ubuntu / Debian
sudo apt install git
```

| 명령어 | 설명 |
|---|---|
| `git --version` | 설치된 Git 버전 확인 |
| `git config --global user.name "이름"` | 커밋 작성자 이름 설정 |
| `git config --global user.email "메일"` | 커밋 작성자 이메일 설정 |
| `git config --global init.defaultBranch main` | 새 저장소의 기본 브랜치명을 `main`으로 설정 |
| `git config --global core.autocrlf true` | 줄바꿈 자동 변환 (Windows 권장) |
| `git config --global core.editor "code --wait"` | 기본 편집기를 VS Code로 설정 |
| `git config --list` | 현재 설정 전체 보기 |
| `git help <command>` | 명령어 도움말 보기 |

---

## 2. 저장소 만들기 / 가져오기

| 명령어 | 설명 |
|---|---|
| `git init` | 현재 디렉터리를 Git 저장소로 초기화 (`.git/` 생성) |
| `git init <이름>` | 새 디렉터리를 만들고 저장소 초기화 |
| `git clone <URL>` | 원격 저장소를 복제 |
| `git clone <URL> <폴더명>` | 지정한 폴더명으로 복제 |
| `git clone --depth 1 <URL>` | 최신 커밋만 얕게 복제 (빠름) |
| `git clone -b <브랜치> <URL>` | 특정 브랜치를 복제 |

---

## 3. 기본 작업 흐름 (변경 → 스테이징 → 커밋)

```
작업 디렉터리  --git add-->  스테이징 영역  --git commit-->  로컬 저장소  --git push-->  원격 저장소
```

### 상태 확인

| 명령어 | 설명 |
|---|---|
| `git status` | 변경된 파일, 스테이징 상태 확인 |
| `git status -s` | 짧은 형식으로 상태 확인 |
| `git diff` | 스테이징 전 변경 내용 보기 |
| `git diff --staged` | 스테이징된(커밋 예정) 변경 내용 보기 |
| `git diff <브랜치1> <브랜치2>` | 두 브랜치 간 차이 비교 |

### 스테이징

| 명령어 | 설명 |
|---|---|
| `git add <파일>` | 특정 파일을 스테이징 |
| `git add .` | 현재 디렉터리의 모든 변경 사항 스테이징 |
| `git add -A` | 삭제를 포함한 모든 변경 사항 스테이징 |
| `git add -p` | 변경 부분(hunk)을 골라서 스테이징 |
| `git restore --staged <파일>` | 스테이징 취소 (변경 내용은 유지) |

### 커밋

| 명령어 | 설명 |
|---|---|
| `git commit -m "메시지"` | 스테이징된 내용으로 커밋 |
| `git commit -am "메시지"` | 추적 중인 파일을 add + commit 한 번에 |
| `git commit --amend` | 직전 커밋 수정 (메시지 또는 내용) |
| `git commit --amend --no-edit` | 메시지는 그대로 두고 직전 커밋에 변경 추가 |

---

## 4. 이력 확인

| 명령어 | 설명 |
|---|---|
| `git log` | 커밋 이력 보기 |
| `git log --oneline` | 한 줄 요약 형식 |
| `git log --oneline --graph --all` | 모든 브랜치를 그래프로 보기 |
| `git log -p <파일>` | 특정 파일의 변경 이력과 내용 |
| `git log -n 5` | 최근 5개 커밋만 보기 |
| `git log --author="이름"` | 특정 작성자의 커밋만 보기 |
| `git show <커밋>` | 특정 커밋의 상세 내용 |
| `git blame <파일>` | 각 줄을 마지막으로 수정한 커밋/작성자 |
| `git reflog` | HEAD 이동 기록 (실수 복구에 유용) |

---

## 5. 브랜치

| 명령어 | 설명 |
|---|---|
| `git branch` | 로컬 브랜치 목록 |
| `git branch -a` | 원격 포함 전체 브랜치 목록 |
| `git branch <이름>` | 새 브랜치 생성 |
| `git switch <이름>` | 브랜치 전환 |
| `git switch -c <이름>` | 새 브랜치를 만들고 전환 |
| `git checkout <이름>` | 브랜치 전환 (구 방식) |
| `git checkout -b <이름>` | 새 브랜치 생성 + 전환 (구 방식) |
| `git branch -m <새이름>` | 현재 브랜치 이름 변경 |
| `git branch -d <이름>` | 병합된 브랜치 삭제 |
| `git branch -D <이름>` | 병합 여부와 관계없이 강제 삭제 |

### 병합 / 리베이스

| 명령어 | 설명 |
|---|---|
| `git merge <브랜치>` | 지정한 브랜치를 현재 브랜치에 병합 |
| `git merge --no-ff <브랜치>` | 항상 병합 커밋을 만들어 병합 |
| `git merge --abort` | 충돌 중인 병합 취소 |
| `git rebase <브랜치>` | 현재 브랜치의 커밋을 지정한 브랜치 위로 재배치 |
| `git rebase --continue` | 충돌 해결 후 리베이스 계속 |
| `git rebase --abort` | 리베이스 취소 |
| `git cherry-pick <커밋>` | 특정 커밋만 현재 브랜치에 적용 |

> **충돌 해결 순서:** 충돌 파일 수정 → `git add <파일>` → `git commit` (merge) 또는 `git rebase --continue` (rebase)

---

## 6. 원격 저장소

| 명령어 | 설명 |
|---|---|
| `git remote -v` | 연결된 원격 저장소 목록 |
| `git remote add origin <URL>` | 원격 저장소 `origin` 추가 |
| `git remote set-url origin <URL>` | 원격 저장소 주소 변경 |
| `git remote remove <이름>` | 원격 저장소 연결 해제 |
| `git fetch` | 원격 변경 사항 가져오기 (병합 안 함) |
| `git fetch --prune` | 원격에서 삭제된 브랜치 정리 |
| `git pull` | fetch + merge |
| `git pull --rebase` | fetch + rebase |
| `git push` | 현재 브랜치를 원격에 업로드 |
| `git push -u origin <브랜치>` | 업스트림을 설정하며 처음 push |
| `git push origin --delete <브랜치>` | 원격 브랜치 삭제 |
| `git push --force-with-lease` | 안전한 강제 push (다른 사람의 변경이 있으면 거부) |

---

## 7. 되돌리기

| 명령어 | 설명 |
|---|---|
| `git restore <파일>` | 작업 디렉터리의 변경 사항 버리기 ⚠️ |
| `git restore --source <커밋> <파일>` | 파일을 특정 커밋 시점으로 복원 |
| `git revert <커밋>` | 해당 커밋을 취소하는 새 커밋 생성 (공유된 이력에 안전) |
| `git reset --soft HEAD~1` | 직전 커밋 취소, 변경 내용은 스테이징 상태로 유지 |
| `git reset HEAD~1` | 직전 커밋 취소, 변경 내용은 작업 디렉터리에 유지 (`--mixed`, 기본값) |
| `git reset --hard HEAD~1` | 직전 커밋과 변경 내용 모두 삭제 ⚠️ |
| `git clean -n` | 추적되지 않는 파일 중 삭제될 목록 미리 보기 |
| `git clean -fd` | 추적되지 않는 파일/폴더 삭제 ⚠️ |

> ⚠️ 표시된 명령은 변경 내용을 되살리기 어렵습니다. 실행 전에 `git status`로 확인하세요.
> 이미 push한 커밋은 `reset` 대신 `revert`로 되돌리는 것이 안전합니다.

---

## 8. 임시 저장 (stash)

| 명령어 | 설명 |
|---|---|
| `git stash` | 현재 변경 사항을 임시 저장하고 작업 디렉터리 정리 |
| `git stash -u` | 추적되지 않는 파일까지 포함해 임시 저장 |
| `git stash push -m "메시지"` | 메시지와 함께 임시 저장 |
| `git stash list` | 임시 저장 목록 |
| `git stash pop` | 가장 최근 stash 적용 후 삭제 |
| `git stash apply stash@{1}` | 특정 stash 적용 (목록에서 유지) |
| `git stash drop stash@{1}` | 특정 stash 삭제 |
| `git stash clear` | 모든 stash 삭제 |

---

## 9. 태그

| 명령어 | 설명 |
|---|---|
| `git tag` | 태그 목록 |
| `git tag v1.0.0` | 가벼운 태그 생성 |
| `git tag -a v1.0.0 -m "릴리스 1.0.0"` | 주석 태그 생성 |
| `git push origin v1.0.0` | 특정 태그 push |
| `git push origin --tags` | 모든 태그 push |
| `git tag -d v1.0.0` | 로컬 태그 삭제 |

---

## 10. .gitignore

Git이 추적하지 않을 파일을 지정합니다. Python + uv 프로젝트 예시:

```gitignore
# 가상환경
.venv/

# Python 캐시
__pycache__/
*.py[cod]

# 빌드 산출물
dist/
build/
*.egg-info/

# 환경 변수 (API 키 등)
.env

# IDE
.vscode/
.idea/
```

| 명령어 | 설명 |
|---|---|
| `git rm --cached <파일>` | 이미 추적 중인 파일을 추적 해제 (파일은 유지) |
| `git check-ignore -v <파일>` | 어떤 규칙 때문에 무시되는지 확인 |

> `uv.lock`, `pyproject.toml`, `.python-version`은 커밋하고, `.venv/`와 `.env`는 커밋하지 않습니다.

---

## 11. GitHub CLI (gh)

| 명령어 | 설명 |
|---|---|
| `gh auth login` | GitHub 계정 로그인 |
| `gh repo create <이름> --private --source . --push` | 현재 폴더로 원격 저장소 생성 후 push |
| `gh repo clone <owner/repo>` | 저장소 복제 |
| `gh pr create` | Pull Request 생성 |
| `gh pr list` | PR 목록 |
| `gh pr checkout <번호>` | PR 브랜치로 전환 |
| `gh pr merge <번호>` | PR 병합 |
| `gh issue list` | 이슈 목록 |

---

## 12. 빠른 시작 예시

```powershell
# 1) 사용자 정보 설정 (최초 1회)
git config --global user.name "홍길동"
git config --global user.email "hong@example.com"

# 2) 저장소 초기화 및 첫 커밋
git init
git add .
git commit -m "Initial commit"

# 3) 기본 브랜치를 main으로
git branch -M main

# 4) 원격 저장소 연결 후 push
git remote add origin https://github.com/<사용자>/<저장소>.git
git push -u origin main

# 5) 기능 브랜치에서 작업
git switch -c feature/llm-chat
# ... 코드 수정 ...
git add .
git commit -m "Add LLM chat feature"
git push -u origin feature/llm-chat

# 6) main에 병합
git switch main
git pull
git merge feature/llm-chat
git push
```

---

## 13. 커밋 메시지 작성 팁

- 첫 줄은 50자 이내로 **무엇을 했는지** 요약합니다.
- 필요하면 한 줄을 비우고 **왜** 했는지 본문에 적습니다.
- 자주 쓰는 접두어 (Conventional Commits):

| 접두어 | 의미 |
|---|---|
| `feat:` | 새 기능 |
| `fix:` | 버그 수정 |
| `docs:` | 문서 변경 |
| `refactor:` | 동작 변화 없는 코드 개선 |
| `test:` | 테스트 추가/수정 |
| `chore:` | 빌드, 설정 등 기타 작업 |

---

## 참고 자료

- 공식 문서: https://git-scm.com/doc
- Pro Git (한국어): https://git-scm.com/book/ko/v2
- GitHub CLI: https://cli.github.com/manual/

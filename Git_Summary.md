# Git & GitHub 실습 요약 및 정리

## 1. Git / GitHub
### 1) Git & GitHub를 사용해야 하는 이유
- **버전 관리(Version Control)를 위해**: 파일이나 코드의 변경 이력을 체계적으로 기록하고 관리함.
  > 언제, 누가, 무엇을 바꿨는지 알 수 있고, 필요하면 과거 상태로 되돌릴 수 있음.

### 2) Git과 GitHub의 차이
- **Git**: 내 컴퓨터에서 동작하는 버전 관리 도구 (변경 내용이 commit 단위로 기록됨)
- **GitHub**: Git 저장소를 올려두는 웹 서비스 & 코드 공유 및 협업 플랫폼
  > Git은 버전 관리 엔진, GitHub는 협업과 공유를 위한 서비스

### 3) Repository (저장소)
- 파일과 변경 이력을 함께 관리하는 저장소
- **로컬 저장소**: 내 컴퓨터에 있는 저장소 (`git init`으로 생성)
- **원격 저장소**: GitHub 서버에 있는 저장소 (`git clone`으로 복사)

### 4) Commit (커밋)
- 변경 사항을 하나의 기록(버전)으로 저장하는 단위
- `git commit -m "커밋 메시지"`

### 5) Branch (브랜치)
- 기존 코드를 건드리지 않고 독립적으로 작업할 수 있는 공간

---

## 2. Git 기본 명령어
- `git config`: 사용자 정보 설정
- `git init`: 현재 폴더를 Git 저장소로 초기화
- `git status`: 저장소 상태 확인
- `git add`: 변경 사항을 Staging Area에 등록
- `git commit`: 스테이징된 변경 사항을 버전으로 기록
- `git push`: 로컬 커밋을 원격 저장소(GitHub)로 업로드
- `git pull`: 원격 저장소의 최신 변경 사항을 불러와 로컬에 병합

---

## 3. Branch & Conflict
### 1) 브랜치 종류 및 역할
- **main**: 배포 가능한 안정 버전
- **develop**: 개발 중인 기능을 합쳐 테스트하는 버전
- **feature/*** : 신규 기능 개발
- **release**: 배포 전 최종 QA 및 버그 수정
- **hotfix/*** : 긴급 버그 수정

### 2) Merge Conflict (충돌) 해결 과정
같은 파일의 같은 부분을 서로 다르게 수정했을 때 충돌이 발생함.
1. 충돌 발생 확인 (`CONFLICT (content)` 메시지 확인)
2. 충돌 파일 내의 기호(`<<<<<<<`, `=======`, `>>>>>>>`) 정리 및 코드 최종 수정
3. `git add <file>` 진행
4. `git commit -m "Fix conflict"`로 병합 완료 커밋 생성

### 충돌 재현 및 해결 실습 예시
```bash
# 1. 저장소 초기화 및 첫 커밋
git init
echo "hello" > test.txt
git add .
git commit -m "first commit"

# 2. feature 브랜치 생성 후 파일 수정
git branch feature
git switch feature
echo "hello from feature" > test.txt
git commit -am "update from feature"

# 3. main 브랜치 이동 후 파일 수정 (충돌 조건 생성)
git switch main
echo "hello from main" > test.txt
git commit -am "update from main"

# 4. 병합 시도 및 충돌 해결
git merge feature
# (VS Code에서 test.txt 파일의 충돌 구문 정리 후 저장)
git commit -am "resolve merge conflict"
git log --oneline --graph
```
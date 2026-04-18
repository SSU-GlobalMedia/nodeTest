# GitHub & Render 배포 가이드

이 문서는 현재 프로젝트를 GitHub에 업로드하고 Render.com을 통해 배포하는 과정을 안내합니다.

## 1. 프로젝트 준비 (이미 완료됨)
이미 다음 작업들을 제가 대신 수행했습니다:
- [x] `.gitignore` 파일 생성 (node_modules, .env 제외)
- [x] `package.json`에 `start` 스크립트 추가
- [x] `server.js`의 포트 설정을 Render 환경에 맞게 최적화

## 2. GitHub에 프로젝트 올리기

### step 1: GitHub 리포지토리 생성
1. [GitHub](https://github.com/)에 로그인합니다.
2. 우측 상단의 **[+]** 버튼을 누르고 **New repository**를 클릭합니다.
3. Repository name을 입력하고 (예: `final-demo-project`), **Create repository** 버튼을 누릅니다. (다른 설정은 건드리지 마세요.)

### step 2: 로컬 터미널에서 Git 명령어 실행
프로젝트 폴더에서 터미널을 열고 다음 명령어를 순서대로 입력하세요:

```bash
# git 초기화
git init

# 파일들 스테이지
git add .

# 첫 커밋
git commit -m "Initial commit for deployment"

# 메인 브랜치 설정
git branch -M main

# 원격 저장소 연결 (username과 reponame을 본인 것에 맞게 수정)
git remote add origin https://github.com/사용자이름/리포지토리이름.git

# GitHub로 푸시
git push -u origin main
```

## 3. Render로 배포하기

### step 1: Render 가입 및 서비스 생성
1. [Render](https://render.com/)에 접속하여 GitHub 계정으로 가입합니다.
2. 대시보드에서 **New +** 버튼을 누르고 **Web Service**를 선택합니다.
3. 이전에 만든 GitHub 리포지토리를 연결(Connect)합니다.

### step 2: 서비스 설정
- **Name**: 프로젝트 이름 입력
- **Environment**: `Node`
- **Build Command**: `npm install`
- **Start Command**: `npm start` (이미 `package.json`에 설정해두었습니다.)

### step 3: 환경 변수(Environment Variables) 설정 (중요!)
`.env` 파일에 있는 내용들을 Render 설정 페이지의 **Environment** 탭에 추가해야 합니다.
1. **Add Environment Variable** 버튼 클릭
2. `DB_URL` : (본인의 몽고DB 연결 문자열)
3. `PORT` : (비워두거나 8080 입력, Render가 자동으로 10000 등으로 할당하기도 함)
4. 기타 `.env`에 있는 모든 키와 값을 하나씩 추가합니다.

### step 4: 배포 확인
설정을 마친 후 **Create Web Service**를 누르면 배포가 시작됩니다. 로그 창에서 `포트 8080으로 서버 대기중 ...` 메시지가 보이면 성공입니다! (실제 접속 주소는 상단에 표시됩니다.)

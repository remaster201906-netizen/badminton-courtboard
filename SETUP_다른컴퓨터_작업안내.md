# 다른 컴퓨터에서 이어서 작업하기

이 폴더(`badminton-courtboard`)를 새 컴퓨터에 풀면 그대로 Git 저장소로 동작합니다. 아래 순서대로 한 번만 준비하면 됩니다.

## 계정 정보

| 항목 | 값 |
| --- | --- |
| GitHub 저장소 | https://github.com/remaster201906-netizen/badminton-courtboard |
| 사이트 (1버전) | https://remaster201906-netizen.github.io/badminton-courtboard/ |
| 사이트 (2버전) | https://remaster201906-netizen.github.io/badminton-courtboard/v2/ |
| Firebase 프로젝트 | `badminton-courtboard` (Firestore 위치: 서울 asia-northeast3) |
| Firebase 콘솔 | https://console.firebase.google.com/project/badminton-courtboard |
| Firebase 로그인 계정 | Firebase 프로젝트를 만든 Google 계정 |

비밀번호나 토큰은 이 압축 파일에 들어 있지 않습니다. 새 컴퓨터에서 아래 3번처럼 다시 로그인해야 합니다.

## 1. 프로그램 설치 (Windows, PowerShell)

```powershell
winget install --id Git.Git -e
winget install --id GitHub.cli -e
winget install --id OpenJS.NodeJS.LTS -e
npm install -g firebase-tools
```

설치 후 PowerShell 창을 닫았다가 다시 엽니다.

## 2. 폴더 풀기

압축을 원하는 위치에 풉니다. 예: `바탕화면\클로드 코드\badminton-courtboard`

압축 대신 GitHub에서 최신본을 받으려면:

```powershell
git clone https://github.com/remaster201906-netizen/badminton-courtboard.git
```

## 3. 로그인 (한 번만)

```powershell
gh auth login          # GitHub.com → HTTPS → 브라우저로 로그인
gh auth setup-git
firebase login         # 브라우저에서 프로젝트를 만든 Google 계정 선택
```

## 4. 최신 상태 맞추기

```powershell
cd "badminton-courtboard"
git pull
```

## 5. 고치고 올리기

화면을 고칠 때는 `index.html`(1버전) 또는 `v2/index.html`(2버전)만 고치면 됩니다.

```powershell
git add -A
git commit -m "무엇을 바꿨는지 한 줄"
git push
```

1~2분 뒤 사이트에 반영됩니다. 브라우저에서 바로 안 바뀌면 새로고침(Ctrl+F5) 하세요.

`firestore.rules`를 고쳤을 때만 추가로 실행합니다.

```powershell
firebase deploy --only firestore:rules
```

## 6. 내 컴퓨터에서 미리 보기

```powershell
npx http-server . -p 8080
```

브라우저에서 http://localhost:8080/v2/ 를 엽니다. 미리 보기에서도 실제 Firebase 데이터에 연결되니, 테스트용 모임을 따로 만들어 쓰고 끝나면 설정 탭에서 삭제하세요.

`firebase-config.js`의 값을 `null`로 바꾸면 체험 모드(그 컴퓨터 안에서만 저장)로 열립니다.

## Claude Code로 이어서 작업할 때

새 컴퓨터의 Claude Code에서 이 폴더를 열고 "README.md와 SETUP 안내를 읽고 이어서 작업해줘"라고 말하면 됩니다.

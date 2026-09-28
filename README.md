# 배드민턴 코트보드

배드민턴 모임에서 쓰는 실시간 팀짜기 보드입니다. 링크를 받은 사람은 누구나 들어올 수 있고, 한 사람이 바꾼 내용이 접속한 모든 사람의 화면에 바로 반영됩니다.

- 방 만들기 / 방 번호로 들어가기
- 닉네임·성별·급수로 입장, 회원 직접 추가
- 코트 자동 배정 (급수 균형 / 남녀 균형 / 랜덤)
- 대기 게임 자동 짜기 (코트가 다 차면 다음 경기 팀을 미리 짜 둠)
- 이름을 눌러 자리 교체, 파트너 바꾸기, 좌우 바꾸기, 코트 이동
- 휴식중(자동 배정에서 빠짐), 퇴장하기

구성: `index.html` 한 파일 + Firebase Firestore(무료 요금제로 충분). 빌드 과정은 없습니다.

---

## 1. Firebase 준비 (한 번만)

1. https://console.firebase.google.com 에 Google 계정으로 들어가 **프로젝트 추가**를 누릅니다. 이름은 자유(예: `badminton-club`), Google 애널리틱스는 꺼도 됩니다.
2. 왼쪽 메뉴 **빌드 > Firestore Database > 데이터베이스 만들기**
   - 위치: `asia-northeast3 (서울)`
   - **프로덕션 모드**로 시작
3. Firestore 화면의 **규칙** 탭을 열고, 이 저장소의 `firestore.rules` 내용을 전부 붙여넣은 뒤 **게시**합니다.
4. 프로젝트 개요 옆 톱니바퀴 > **프로젝트 설정 > 일반 > 내 앱**에서 웹(`</>`) 아이콘으로 앱을 등록합니다. (Firebase 호스팅 체크는 필요 없음)
5. 화면에 나오는 `firebaseConfig = { ... }` 값을 복사해 `firebase-config.js`의 `window.FIREBASE_CONFIG = null;` 자리에 붙여넣습니다.

```js
window.FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "badminton-club.firebaseapp.com",
  projectId: "badminton-club",
  storageBucket: "badminton-club.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef"
};
```

> `apiKey`는 비밀번호가 아니라 공개 식별자라서 GitHub에 올려도 됩니다. 데이터 보호는 3번의 보안 규칙이 합니다.

설정 전(`null`)에는 **체험 모드**로 열립니다. 그 기기 안에서만 저장되고 다른 사람과 공유되지 않습니다.

## 2. GitHub Pages로 공개

1. GitHub에 새 저장소를 만들고(Public) 이 폴더의 파일을 올립니다.
   - `index.html`, `firebase-config.js`, `firestore.rules`, `README.md`, `.nojekyll`
2. 저장소 **Settings > Pages**
   - Source: **Deploy from a branch**
   - Branch: `main` / `/ (root)` 선택 후 **Save**
3. 1~2분 뒤 `https://<GitHub아이디>.github.io/<저장소이름>/` 주소로 열립니다. 이 주소를 모임 단톡방에 공유하세요.

방 안에서 방 번호를 누르면 `…/#room-1234` 형태의 바로가기 링크가 복사됩니다.

## 3. 수정하고 다시 올리기

`index.html`을 고친 뒤 GitHub에 다시 올리면(커밋/푸시) 1~2분 안에 사이트가 바뀝니다.

## 알아둘 점

- 로그인 없는 공개 보드입니다. 링크(또는 방 번호)를 아는 사람은 누구나 팀을 바꾸거나 회원을 퇴장시킬 수 있어요. 모임 안에서만 링크를 공유하세요.
- 운동이 끝나면 **방 설정 > 방 닫기**로 방을 지우면 기록이 정리됩니다.
- Firestore 무료 한도(하루 읽기 5만 / 쓰기 2만 회)는 30~40명 규모 모임이 매일 써도 넉넉합니다.

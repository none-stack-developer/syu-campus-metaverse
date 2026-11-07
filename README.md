# 삼육대학교 메타버스

브라우저에서 돌아다니는 3D 캠퍼스 메타버스. 파일 하나(`sahmyook.html`)로 동작하고, three.js는 CDN에서 불러온다.

- **배포 주소의 첫 화면(`/`)** = `sahmyook.html` (캠퍼스, 온라인 멀티플레이)
- **`/cafe.html`** = `index.html` (초대형 무인카페, 혼자 하는 버전)

배포 때 `vercel.json`의 빌드 명령이 두 파일을 `dist/`에 위 이름으로 복사한다. 로컬에서는 파일을 더블클릭해서 열면 된다.

## 온라인 (Firebase Realtime Database)

닉네임을 입력하고 들어오면 같은 주소로 접속한 사람들이 서로 보이고 채팅할 수 있다. 로그인은 없다.

- 접속자 위치·자세는 `rooms/syu-campus/players/{id}`, 채팅은 `rooms/syu-campus/chat`에 저장된다. 창을 닫으면 접속자 기록은 서버가 지운다(onDisconnect).
- 같은 건물·같은 층·같은 방에 있는 사람만 화면에 보인다.
- 데이터베이스에 연결하지 못하면 "혼자 모드"로 계속 동작한다.

### 데이터베이스 준비 (한 번만)

1. Firebase 콘솔 → 프로젝트 `metaverse-658b1` → **빌드 › Realtime Database › 데이터베이스 만들기** (위치는 아무거나. 코드가 미국·싱가포르·벨기에 주소를 차례로 찾는다)
2. **규칙** 탭에 `database.rules.json` 내용을 붙여 넣고 **게시**

규칙은 `rooms/*/players`와 `rooms/*/chat`만 읽고 쓰게 열어 두고, 이름 16자·채팅 120자 제한과 채팅 수정·삭제 금지를 검사한다.

## 출처

- 지도 데이터 © OpenStreetMap contributors (ODbL)
- 건물·층별 안내: 삼육대학교 캠퍼스맵
- 학식 메뉴: SYU CAMPUS(campus.syu.kr) SU-Lounge 주간 식단 (2026.11.02~11.06)

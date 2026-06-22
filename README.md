# 경주 여행 플래너 🏯

1박 2일 경주 여행을 위한 PWA 웹앱입니다.
실시간 위치·시간 기반으로 동선을 추천하고, 웨이팅 현황을 확인할 수 있어요.

## 기능

- 📍 **현재 위치 기반 동선 추천** — GPS로 가장 가까운 다음 일정을 하이라이트
- ⏰ **실시간 시계 + D-day** — 여행일 카운트다운
- 🔔 **웨이팅 현황** — 온목당(캐치테이블 연동) + 현장 웨이팅 가능 여부 표시
- 📱 **PWA** — 홈 화면에 추가하면 앱처럼 사용 가능
- 🌐 **오프라인 지원** — 한 번 열면 인터넷 없이도 동작

---

## GitHub Pages로 배포하는 방법

### 1단계 — 레포지토리 만들기

1. [github.com](https://github.com) 로그인
2. 우측 상단 **+** → **New repository**
3. Repository name: `gyeongju-planner`
4. **Public** 선택 → **Create repository**

### 2단계 — 파일 업로드

방법 A (웹에서 직접):
1. 레포지토리 페이지에서 **Add file** → **Upload files**
2. 이 폴더의 파일을 모두 드래그 앤 드롭
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icons/` 폴더 전체
3. **Commit changes**

방법 B (터미널):
```bash
git clone https://github.com/YOUR_USERNAME/gyeongju-planner
cp -r ./* gyeongju-planner/
cd gyeongju-planner
git add .
git commit -m "첫 배포"
git push
```

### 3단계 — GitHub Pages 활성화

1. 레포지토리 → **Settings** 탭
2. 왼쪽 메뉴 **Pages**
3. Source: **Deploy from a branch**
4. Branch: **main** / **/ (root)** 선택 → **Save**
5. 잠시 후 `https://YOUR_USERNAME.github.io/gyeongju-planner` 로 접속 가능

### 4단계 — 폰에 앱으로 설치

**iPhone (Safari)**:
1. Safari에서 위 URL 열기
2. 하단 공유 버튼(□↑) → **홈 화면에 추가**
3. 이름 확인 후 **추가**

**Android (Chrome)**:
1. Chrome에서 URL 열기
2. 상단 주소창 옆 **⋮** → **홈 화면에 추가**
   또는 하단에 자동으로 "앱 설치" 배너가 뜸

---

## 여행일 변경 방법

`index.html`에서 아래 부분만 바꾸면 돼요:

```javascript
// 약 340번째 줄 근처
const d27 = new Date(2026, 5, 27); // 6월 27일 → 월(0부터 시작)이므로 5=6월
const d28 = new Date(2026, 5, 28); // 6월 28일
```

그리고 헤더의 날짜 텍스트도 바꿔주세요:
```html
<div class="ht">1박 2일<br>06.27 토 – 28 일</div>
```

---

## 일정 변경 방법

`index.html`의 `SCHED_D1`, `SCHED_D2` 배열을 수정하면 돼요.

```javascript
const SCHED_D1 = [
  { time:'10:00', key:'station', name:'경주역 도착', sub:'KTX 하차', dot:'s', badge:'bgray', badgeTxt:'출발', tags:[] },
  // 여기에 장소 추가/수정
];
```

`key` 값은 `PLACES` 객체의 키와 일치해야 GPS 위치 매칭이 돼요.

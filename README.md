# 📚 사서의 언어 서재 — 구조 가이드

## 📁 파일 구성

```
librarian-language-app/
├── index.html              ← 앱 본체 (코드만, 데이터 없음)
├── data/
│   ├── hanja.js            ← 한자 96자
│   ├── chinese.js          ← 중국어 회화 60문장
│   ├── japanese.js         ← 일본어 회화 59문장
│   ├── pron.js             ← 영국 RP 발음 38개
│   ├── english.js          ← 영국 영어 회화 52문장
│   ├── opic_topics.js      ← OPIc 주제 12개
│   ├── opic_scripts.js     ← OPIc 스크립트 (IM/IH/AL)
│   ├── interview.js        ← 면접 Q&A 13개
│   └── wordbook.js         ← 내 단어장 (직접 편집)
└── README.md
```

---

## ✍️ 데이터 추가 방법

### 방법 1 — 앱 안에서 직접 추가 (소량)
`📓 내 단어장` 탭 → 앞면/뒷면 입력 → ＋ 추가  
→ 브라우저 localStorage에 저장 (앱 닫아도 유지)

### 방법 2 — 파일 직접 편집 (대량 추가, 추천)

#### `data/wordbook.js` 편집 예시
```js
export const WORDBOOK_DATA = [
  {
    front: '정보리터러시',
    back: 'Information Literacy',
    category: '📚 사서 핵심개념',
    lang: 'ko',
    note: 'ACRL Framework 기반'
  },
  {
    front: '書架',
    back: 'shūjià (中) / しょか (日)',
    category: '漢 한자',
    lang: 'zh',
    note: '書(글 서) + 架(시렁 가)'
  },
  // ... 계속 추가
];
```

#### `data/chinese.js` 문장 추가 예시
```js
// 기존 카테고리에 항목 추가
{ cat: '📚 도서관 기본', items: [
  // 기존 항목들...
  { zh: '新文章', py: 'xīn wénzhāng', ko: '새 문장', tip: '설명' },  // ← 추가
]},
```

### 방법 3 — JSON 내보내기/가져오기 (기기 간 이동)
내 단어장 탭 → `📥 JSON 내보내기` → 다른 기기에서 `📤 JSON 가져오기`

---

## 🚀 배포 방법

### GitHub Pages (무료, 추천)

```bash
# 1. 저장소 생성 후
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/[아이디]/[저장소명].git
git push -u origin main
```

Settings → Pages → Source: `GitHub Actions`  
`.github/workflows/deploy.yml` 파일이 있으면 자동 배포됩니다.

**접속 URL:** `https://[아이디].github.io/[저장소명]/`

### 로컬 테스트 (HTTPS 필요 — 모듈 import 때문)

```bash
npx serve .
# 또는
python3 -m http.server 8080
```
→ `http://localhost:8080` 에서 열기

> ⚠️ `file://` 로 직접 열면 ES module import가 차단됩니다.  
> 반드시 로컬 서버나 배포 환경에서 사용하세요.

---

## 🔮 나중에 Supabase 연동 시 (향후 계획)

지금 `localStorage` 에 저장된 데이터는 JSON 형식이라
Supabase로 마이그레이션할 때 그대로 import 가능합니다.

```
현재: localStorage → JSON export → Supabase import
미래: 앱에서 Supabase 직접 읽기/쓰기
```

마이그레이션 시 `data/wordbook.js` 포맷도 동일하게 유지됩니다.

---

## ⭐ 즐겨찾기 & 학습 현황

- 즐겨찾기: localStorage에 저장 (`libFavorites` 키)
- 내 단어장: localStorage에 저장 (`libWordbook` 키)
- API 키: localStorage에 저장 (`msApiKey` 키)
- 교정 히스토리: localStorage에 저장 (`scriptHistory` 키)

모두 브라우저 기준 저장이라 기기를 바꾸면 초기화됩니다.  
중요한 데이터는 주기적으로 JSON 내보내기 해두세요.

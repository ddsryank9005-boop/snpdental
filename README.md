# S&P 치과의원 홈페이지

에스앤피 치과의원(S&P Dental Clinic) 홈페이지입니다. 빌드 과정 없이 그대로 배포하는 정적 HTML 사이트이며, [Vercel](https://vercel.com)로 배포합니다.

## 구성

| 파일 | 내용 |
|---|---|
| `index.html` | 메인 페이지 (운영시간 · 진료 안내 · 예약 안내 · 위치/주차 · 질문과 답) |
| `story.html` | 기준과 원칙 · S&P 이야기 |
| `treatment-notice.html` | 치료 후 주의사항 |
| `404.html` | 없는 주소로 들어왔을 때 보이는 안내 페이지 |
| `img/` | 사진, 배경 질감, 로고, 메인 영상(PC 가로형 · 모바일 세로형) |
| `favicon.ico`, `apple-touch-icon.png` | 브라우저 탭 · 홈 화면 아이콘 |
| `vercel.json` | Vercel 설정 (캐시 · 보안 헤더) |
| `robots.txt` | 검색엔진 수집 허용 |

- 한국어 / English / 日本語 / 中文 전환은 각 페이지 안에서 이루어집니다(새 창 없음).
- 카카오톡 상담, 예약, 치료 후 주의사항, S&P 이야기 링크는 새 창으로 열립니다.

## Vercel 배포

1. Vercel → **Add New… → Project** → 이 저장소(`snpdental`) **Import**
2. 설정
   - **Framework Preset**: `Other`
   - **Root Directory**: `./` (그대로)
   - **Build Command**: 비워 둠 (빌드 없음)
   - **Output Directory**: 비워 둠 (저장소 루트를 그대로 배포)
   - **Install Command**: 비워 둠
3. **Deploy**

이후 `main` 브랜치에 커밋하면 자동으로 다시 배포됩니다.

### vercel.json 설정 내용

| 대상 | 설정 |
|---|---|
| `/img/*` | 7일 캐시 (`max-age=604800`) + 하루 동안 이전 파일로 먼저 보여주고 뒤에서 갱신 |
| `favicon.ico`, `apple-touch-icon.png` | 7일 캐시 |
| 모든 페이지 | `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin` |

HTML은 Vercel 기본값(매번 최신 확인)을 따르므로, 글을 고치면 바로 반영됩니다.
사진·영상을 **같은 파일명으로 교체**하면 방문자 브라우저에 최대 7일간 이전 파일이 남을 수 있으니, 교체할 때는 파일명을 바꾸고(예: `hero-land-2.mp4`) HTML의 경로도 함께 바꿔 주세요.

### 도메인 연결 후 할 일

- Vercel → Project → **Settings → Domains**에서 도메인을 연결합니다.
- 도메인이 정해지면 세 HTML 파일의 `og:image`를 절대 주소로 바꿔 주세요.
  카카오톡 · 페이스북 링크 미리보기는 상대 경로(`img/og.jpg`)를 읽지 못합니다.
  ```html
  <meta property="og:image" content="https://도메인/img/og.jpg">
  ```

## 로컬에서 보기

```bash
python3 -m http.server 8000
# http://localhost:8000
```

메인 영상은 `fetch`로 불러오므로 파일을 더블클릭해 여는 것보다 위처럼 로컬 서버로 여는 것이 정확합니다.

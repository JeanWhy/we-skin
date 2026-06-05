# WE SKIN 랜딩 페이지 — 작업 기록 (Build Log)

> i-Beauty Chatswood(Sydney, NSW) 내 스킨·뷰티 스튜디오 **WE SKIN**의 원페이지 랜딩 사이트 제작 기록.
> 운영: Oko(테라피스트/오너) · 개발: Jean

**라이브:** https://www.we-skin.com (백업: https://we-skin.vercel.app)

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| 형태 | 단일 정적 페이지 (`index.html`, 빌드 과정 없음) |
| 레이아웃 | 폰 컬럼 중심 (`--max: 480px`), 모바일 우선 |
| 폰트 | Cormorant Garamond(세리프) + Inter(산세리프) |
| 색상 | 화이트 배경 + 골드 액센트 (`#c4a14e` / `#9c7c2f`) |
| 언어 | 영어 / 몽골어 이중언어 (브라우저 언어 자동 감지) |
| 예약 | Square Appointments 연동 |
| 비용 | 호스팅 $0 + 도메인 약 $10/년 |

---

## 2. 기술 스택 & 인프라

- **GitHub** — 레포 `JeanWhy/we-skin` (public, `main` 브랜치). 소스 보관 + 배포 트리거.
- **Vercel** — GitHub에 push하면 자동으로 빌드·배포 (약 1~2분).
- **Cloudflare** — 도메인 등록(`we-skin.com`) + DNS 관리.
  - DNS: `CNAME` 레코드 `www` → Vercel 주소, **Proxy 끔(DNS only, 회색 구름)** — SSL 충돌 방지에 중요.
- **로컬 작업 폴더:** `/Users/jean/Documents/Claude/Projects/WeSkin` (Mac, zsh)

---

## 3. 배포 워크플로우 (매 수정 시)

```bash
cd /Users/jean/Documents/Claude/Projects/WeSkin
git add index.html [+ 새 이미지/영상 파일]
git commit -m "변경 내용 요약"
git push
```

**핵심 교훈**
- 작업 파일 `we-skin-minimal.html`을 항상 `index.html`로 복사한 뒤 배포.
- 새 이미지·영상 자산은 반드시 함께 `git add` — 빠지면 배포 후 404.
- `git add`만 하고 `git commit`을 빼먹으면 push해도 아무것도 안 올라감. (실제로 한 번 겪음)
- 배포 확인: GitHub 커밋 수 증가 + 커밋 옆 초록 체크(✓) = Vercel 배포 성공. 사이트는 하드 새로고침(Cmd+Shift+R).

---

## 4. 수행한 작업

### 4-1. 인프라 구축
- GitHub 레포 생성 및 Vercel 연결, Cloudflare 도메인 등록·DNS 설정으로 `we-skin.com` 라이브.
- IP Australia에서 "we-skin" 상표 충돌 없음 확인.

### 4-2. 페이지 구조 & 디자인
- 섹션 순서: 네비 → Hero → 액션 버튼 → 스튜디오 영상 → About → Treatment Menu → Trust → Reviews → 스튜디오 영상(하단) → Info → Footer.
- EN/MN 다국어 시스템: `I18N` 객체 + `data-i18n` 속성 + `setLang()`. `navigator.languages`로 몽골어 사용자 자동 감지, 수동 선택은 localStorage에 저장.

### 4-3. Hero & 브랜딩
- 골드 링 로고(`hero-ring.png`)를 Hero 배경으로 배치, 농도(opacity) `.5`로 은은하게 조정.
- BOOK NOW(검정) / OUR SERVICES(골드 외곽선) 버튼을 링 하단 곡선에 살짝 겹치게 배치.
- Hero 아래 스튜디오 시술 영상(`studio.mp4`) 자동재생(음소거·무한반복).

### 4-4. 네비게이션
- 모바일(≤640px)에서 항목이 잘리는 문제 → **햄버거 메뉴**로 전환.
- 데스크톱은 가로 네비 유지. EN/MN 토글은 모바일 바에서 햄버거 왼쪽에 상시 노출.

### 4-5. 콘텐츠
- **몽골어 카피**: Oko가 다듬은 문구로 Hero 소개문·About·후기 반영.
- **고객 후기**: 실제 구두 후기 기반으로 확정(별도 교체 불필요).
- **서비스 메뉴**: Square 최신 목록과 동기화.
  - 11개 서비스, 가격·설명을 Square 공식 내용으로 영어·몽골어 모두 일치.
  - 신규 서비스 **Acne Treatment($150)**, **Laser Skin Rejuvenation($350)** 추가.
  - 모든 서비스가 각자의 Square 예약 페이지로 직접 연결.

### 4-6. 미디어 (영상)
- 하단 스튜디오 사진 자리 2칸을 **실제 마사지 영상**으로 교체.
- **클릭 재생** 방식(자동재생 X) — 정지 시 썸네일(poster) + 플레이 버튼, 무한 자동재생 부담 제거.
- 두 영상의 밝기/톤 차이를 CSS 필터로 보정.
- 루프 시 깜빡임의 원인이던 **검은 프레임**(영상 앞/끝)을 ffmpeg로 제거.

### 4-7. 소셜 & 연락 채널 (Footer + 플로팅)
- **Facebook** 링크
- **Instagram** 링크
- **SMS(문자)** 링크 — 누르면 번호와 메시지("Hi WE SKIN, I'd like to book an appointment.")가 미리 채워진 채로 문자 앱 실행.
- **WhatsApp** 플로팅 버튼, **전화** 버튼.
- 푸터에 카피라이트 `© 2026 WE SKIN · Chatswood, NSW`.

### 4-8. 예약 정책 (Square + 사이트)
- **Deposit:** 전 서비스 일괄 **$20** (서비스 비용에서 차감).
- **취소 cut-off:** **12시간** — 12시간 전 취소/변경 시 환불·이월, 그 이후 또는 노쇼 시 deposit 소멸.
- 정책 문구를 "Book online" 버튼 아래에 영어·몽골어로 노출, Square 취소 정책에도 동일 적용.

### 4-9. 문서화
- 영어 `README.md` 작성.
- 본 작업 기록(`WE-SKIN-Build-Log.md`) 작성.

---

## 5. 파일 구성

| 파일 | 역할 |
|------|------|
| `we-skin-minimal.html` | 마스터 작업 파일 (편집용) |
| `index.html` | 배포본 (작업 파일을 복사) |
| `hero-ring.png` | Hero 골드 링 로고 |
| `studio.mp4` | Hero 아래 자동재생 영상 |
| `massage1.mp4` / `massage2.mp4` | 하단 클릭 재생 영상 |
| `massage1-poster.jpg` / `massage2-poster.jpg` | 영상 썸네일 |
| `README.md` | 프로젝트 안내 (영어) |

---

## 6. 남은 할 일 / 향후 아이디어

- [ ] `README.md`를 GitHub에 올리기.
- [ ] 몽골어 번역(서비스 설명·정책 문구)을 Oko가 최종 검수.
- [ ] 영어/몽골어 후기 내용이 일부 다름 — 통일 여부 결정(현재는 각 언어대로 유지).
- [ ] SMS 미리 채움 메시지를 언어별로 분기할지 검토(현재 영어 고정).
- [ ] deposit: 고가 서비스(IPL/Laser/Nano) 노쇼가 잦아지면 그 항목만 비율 상향 검토.

---

*최종 업데이트: 2026-06 · 작성 참고용 내부 문서*

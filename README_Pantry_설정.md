# Pantry 설정 가이드 (3분 소요)

GitHub Pages에서 신청을 받고 관리자 페이지에서 확인하기 위해
**Pantry** (무료 JSON 저장소)를 사용합니다. 가입 1분이면 끝.

---

## 1단계 — Pantry ID 발급 받기

1. https://getpantry.cloud 접속
2. 화면에 "Get Started" 또는 이메일 입력 칸이 있음
3. **본인 이메일 입력** (예: dendeal28@gmail.com)
4. **Pantry name** 입력 (예: dendeal-advisors) — 영문/숫자만
5. **Create Pantry** 클릭
6. 이메일로 **Pantry ID** 가 발송됨
   - 다음과 같은 UUID 형식: `abc12345-6789-defg-hijk-lmnopqrstuvw`
7. 이메일에 있는 링크를 클릭해서 Pantry 대시보드 진입 (확인용)

> 💡 별도의 비밀번호나 로그인이 없습니다. 이메일로 받은 Pantry ID 자체가 키 역할을 합니다.

---

## 2단계 — HTML 파일 2개에 Pantry ID 붙여넣기

### A. `혜택신청.html` 수정

메모장으로 열어서 다음 줄을 찾아주세요 (Ctrl + F → `REPLACE_WITH`):

```js
const PANTRY_ID = 'REPLACE_WITH_YOUR_PANTRY_ID';
```

`REPLACE_WITH_YOUR_PANTRY_ID` 부분을 1단계에서 받은 Pantry ID 로 교체:

```js
const PANTRY_ID = 'abc12345-6789-defg-hijk-lmnopqrstuvw';
```

저장 후 닫기.

### B. `관리자.html` 수정

같은 방법으로 다음 두 줄 수정:

```js
const PANTRY_ID = 'REPLACE_WITH_YOUR_PANTRY_ID';      // ← 위와 동일한 ID
const ADMIN_PASSWORD = 'dendeal_admin_2025';           // ← 본인이 정한 비밀번호로 변경 권장
```

`ADMIN_PASSWORD` 는 관리자 페이지 접속용 비밀번호입니다.
본인이 기억할 수 있는 안전한 값으로 변경해주세요.

저장 후 닫기.

---

## 3단계 — Git 푸시 (배포)

PowerShell 또는 Git Bash 에서:

```bash
cd "D:\홍보\영업용실장님용"
git add .
git commit -m "혜택 신청 + 관리자 페이지 추가 (Pantry 연동)"
git push
```

1~2분 뒤 GitHub Pages 에 자동 반영됩니다.

---

## 4단계 — 테스트

### 신청 페이지 테스트
1. https://kswmiso0691.github.io/dendeal-promo/혜택신청.html 접속
2. 테스트 데이터로 신청
3. "신청이 완료되었습니다" 팝업이 뜨면 성공

### 관리자 페이지 확인
1. https://kswmiso0691.github.io/dendeal-promo/관리자.html 접속
2. 2단계에서 설정한 비밀번호 입력
3. 방금 테스트한 신청이 표 형태로 보이면 성공!

---

## 📊 관리자 페이지 기능

| 기능 | 설명 |
|------|------|
| 전체/오늘/대기/연락완료/승인/거절 | 자동 통계 카드 |
| 신청 목록 | 신청일시, 병원명, 원장님, 연락처 (전화 클릭 가능) |
| 상태 변경 | 드롭다운 → 자동 저장 (대기 → 연락완료 → 승인/거절) |
| 메모 | 자유 입력 → 포커스 빠질 때 자동 저장 |
| 삭제 | 항목별 삭제 가능 (확인 메시지 후) |
| 새로고침 | 최신 데이터 다시 불러오기 |
| CSV 다운로드 | 엑셀에서 열 수 있는 파일 |
| 로그아웃 | 비밀번호 다시 입력해야 함 |

스마트폰 브라우저에서도 잘 보입니다.

---

## ⚠️ 보안 안내

- **Pantry ID** 는 HTML 코드 안에 들어 있어서 누군가 페이지 소스를 보면 알 수 있습니다.
  → 누군가 가짜 신청을 마구 넣을 가능성이 있습니다. 100곳 모집 정도는 수동으로 걸러낼 수 있습니다.
- **관리자 비밀번호** 도 클라이언트에서 검증하므로 강력한 보안은 아닙니다.
  → 소스에서 비밀번호가 보입니다. **민감한 정보용으로는 부적절**합니다.
- 더 강력한 보안이 필요하면 Supabase 같은 진짜 인증 서비스로 옮길 수 있습니다.

---

## 🔧 자주 묻는 질문

**Q. Pantry ID를 잊어버렸어요.**
A. https://getpantry.cloud 에서 가입 시 입력한 이메일로 다시 받을 수 있습니다.

**Q. Pantry 무료 한도?**
A. 월 10,000 회 요청. 본 용도(연간 100건 신청)로는 사실상 무한대입니다.

**Q. 데이터를 완전히 초기화하고 싶어요.**
A. 관리자 페이지에서 모든 항목을 삭제하시거나, 새 Pantry ID 를 발급받으세요.

**Q. 같은 사람이 두 번 신청해도 막을 수 없나요?**
A. 현재는 막지 않습니다. 관리자 페이지에서 수동으로 중복 신청을 확인/삭제하시면 됩니다.

**Q. 알림 이메일도 받고 싶어요.**
A. Pantry 자체는 알림 기능이 없습니다. 알림이 필요하면 별도 자동화(Zapier 등)가 필요합니다.

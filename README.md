# 💰 가계부 API (FastAPI + Supabase PostgreSQL)

- **GitHub 저장소 주소**: https://github.com/jeehoshin/ledger-api
- **Render 배포 주소**: https://ledger-api-1a3h.onrender.com

---

## 1. 과제 결과 확인
- **Supabase 연동**: FastAPI 애플리케이션과 클라우드 PostgreSQL(Supabase)을 연결하여 계좌 및 거래 데이터를 클라우드에 영구 저장.
- **Render 클라우드 배포**: 로컬 환경을 벗어나 Render 웹 서비스를 통해 전 세계 어디서나 접근 가능한 REST API 엔드포인트 제공.

---

## 2. 핵심 개념 되새김

1. **계좌와 거래를 두 테이블로 나눈 이유 (1:N 관계)**:
   - 한 계좌는 여러 건의 거래 내역을 가질 수 있으므로, 데이터를 분리하여 중복을 없애고(정규화) 각 거래 내역의 변경 및 조회를 독립적이고 안전하게 관리하기 위함.

2. **SQLAlchemy 모델 클래스와 실제 DB 테이블의 대응**:
   - 파이썬 클래스(`Account`, `Transaction`)와 타입 어노테이션이 DB의 물리적 테이블(`accounts`, `transactions`) 및 컬럼 속성과 1:1로 매핑되어, 직접 SQL 쿼리를 작성하지 않고도 파이썬 객체 조작만으로 DB CRUD를 수행할 수 있음.

3. **접속 문자열(`DATABASE_URL`)을 `.env`로 분리하는 이유**:
   - DB 호스트, 포트, 계정 및 비밀번호와 같은 민감한 보안 정보를 소스코드에 하드코딩하지 않고 보호하기 위함.
   - 로컬 개발 환경과 배포 환경(Render 환경변수)에서 코드 수정 없이 환경변수 교체만으로 DB 대상을 유연하게 전환하기 위함.

---

## 3. 자유 로그 (학습 회고)
- **배운 점 및 해결 과정**:
  - 로컬 환경과 클라우드 배포 환경의 DB 드라이버 차이(`psycopg` vs `psycopg2`)를 사전에 점검하고 `postgresql+psycopg://` 형식의 중요성을 이해함.
  - FastAPI의 의존성 주입(`Depends(get_db)`)을 통해 세션 누수를 방지하는 구조를 체화함.
- **AI 활용 및 검증**:
  - AI 어시스턴트와 함께 로컬 DB 연결 상태 및 테이블 데이터 존재 여부를 검증하고, `.gitignore` 설정을 통해 민감한 `.env` 파일이 Git에 추적되지 않도록 사전에 점검함.

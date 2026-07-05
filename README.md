<div align="center">

  <img src="https://fesnote.vercel.app/fesnote_logo.png" width="86" alt="FesNote 로고" />

  # FesNote

  공연을 기록하고, 다시 보고, 함께 채워가는 공연 캘린더

  <p>
    <a href="https://fesnote.vercel.app"><img src="https://img.shields.io/badge/Service-fesnote.vercel.app-D96C96?style=for-the-badge" alt="서비스" /></a>
    <a href="https://fesnote.onrender.com/api/health"><img src="https://img.shields.io/badge/API-Render-111827?style=for-the-badge" alt="API" /></a>
    <img src="https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=111111" alt="React" />
    <img src="https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" alt="Node.js" />
    <img src="https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB" />
  </p>

</div>

## 개요

FesNote는 공연 관람 기록을 캘린더와 통계로 관리하는 웹 애플리케이션입니다.

직접 본 공연을 남기고, KOPIS, 서울 열린데이터광장, 공공데이터포털의 공연/문화 데이터를 불러오며, 다른 사용자가 추가한 공연도 내 기록에 담을 수 있습니다.

## 배포 주소

| 구분 | URL |
| --- | --- |
| 프론트엔드 | https://fesnote.vercel.app |
| 백엔드 | https://fesnote.onrender.com |

## 주요 기능

- 공연 기록 추가, 수정, 삭제
- 월별 캘린더 기반 내 관람 기록 조회
- 올해 관람 횟수, 지출, 최다 관람 아티스트, 페스티벌 횟수 요약
- KOPIS, 서울 열린데이터광장, 공공데이터포털 기반 공연/문화 정보 가져오기
- 사용자가 추가한 공연을 내 기록에 담기
- 이메일 인증 회원가입과 비밀번호 로그인
- JWT 기반 인증 유지로 모바일/데스크톱 사용 안정화
- 게시판 기반 공지와 피드백 관리
- 모바일 브라우저 대응

## 기술 스택

| 영역 | 기술 |
| --- | --- |
| 프론트엔드 | React, Axios, CSS |
| 백엔드 | Node.js, Express, Passport, JWT |
| 데이터베이스 | MongoDB Atlas, Mongoose |
| 이메일 | Resend API, SMTP fallback |
| 배포 | Vercel, Render |
| 외부 API | KOPIS, 서울 열린데이터광장, 공공데이터포털 |

## 아키텍처

```txt
클라이언트 (Vercel)
  └─ React 앱
      └─ Axios + JWT Authorization header

API 서버 (Render)
  ├─ Express 라우트
  ├─ Passport 세션 fallback
  ├─ JWT 인증 미들웨어
  ├─ Resend 이메일 인증
  └─ KOPIS, 서울 열린데이터광장, 공공데이터포털 연동

데이터베이스 (MongoDB Atlas)
  ├─ Users
  ├─ Concerts
  ├─ PendingAuth
  ├─ Artists
  ├─ Venues
  └─ BoardPosts
```

## 프로젝트 구조

```txt
fesnote/
├── backend/
│   ├── controllers/        # 공연 및 게시판 비즈니스 로직
│   ├── middleware/         # 인증 미들웨어
│   ├── models/             # MongoDB 모델
│   ├── routes/             # API 라우트
│   ├── services/           # 이메일, 외부 데이터, 아티스트, 공연장 서비스
│   ├── scripts/            # 마이그레이션 스크립트
│   └── server.js
├── frontend/
│   ├── public/
│   └── src/
│       ├── components/     # 캘린더, 폼, 카드, 통계, 게시판 컴포넌트
│       ├── App.js
│       └── index.js
└── README.md
```

## 시작하기

### 백엔드 실행

```bash
cd backend
npm install
cp .env.example .env
npm run dev
```

백엔드는 `http://localhost:5001`에서 실행됩니다.

### 프론트엔드 실행

```bash
cd frontend
npm install
npm start
```

프론트엔드는 `http://localhost:3000`에서 실행됩니다.

## 환경변수

### 백엔드

```env
MONGODB_URI=mongodb://localhost:27017/fesnote
PORT=5001
FRONTEND_URL=http://localhost:3000
SESSION_SECRET=change-me
JWT_SECRET=change-me

KOPIS_API_KEY=

RESEND_API_KEY=
RESEND_FROM=FesNote <onboarding@resend.dev>

SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=
SMTP_PASS=
SMTP_FROM=

SEOUL_OPEN_DATA_API_KEY=
DATA_GO_KR_API_KEY=
DATA_GO_KR_API_URL=
MUSICBRAINZ_USER_AGENT=FesNote/1.0 (mailto:you@example.com)
```

### 프론트엔드

```env
REACT_APP_API_URL=http://localhost:5001
```

운영 환경에서는 아래 값을 사용합니다.

```env
REACT_APP_API_URL=https://fesnote.onrender.com
```

## 배포

### Vercel

```txt
Root Directory: frontend
Install Command: npm install
Build Command: npm run build
Output Directory: build
```

필수 환경변수:

```env
REACT_APP_API_URL=https://fesnote.onrender.com
```

### Render

```txt
Root Directory: backend
Build Command: npm install
Start Command: npm start
```

필수 환경변수:

```env
NODE_ENV=production
MONGODB_URI=mongodb+srv://...
FRONTEND_URL=https://fesnote.vercel.app
SESSION_SECRET=long-random-string
JWT_SECRET=long-random-string
RESEND_API_KEY=re_...
RESEND_FROM=FesNote <onboarding@resend.dev>
```

MongoDB Atlas를 사용하는 경우, Render에서 접근할 수 있도록 Network Access 설정이 필요합니다.  
초기 테스트 단계에서는 `0.0.0.0/0` 설정이 가장 간단합니다.

## 인증 흐름

1. 사용자가 이메일 인증번호를 요청합니다.
2. 회원가입 대기 데이터가 MongoDB의 `PendingAuth`에 10분 동안 저장됩니다.
3. 사용자가 이메일과 인증번호를 입력해 인증을 완료합니다.
4. 백엔드가 사용자를 생성하거나 기존 정보를 업데이트하고 JWT를 반환합니다.
5. 프론트엔드는 토큰을 `localStorage`에 저장합니다.
6. 이후 API 요청에는 `Authorization: Bearer <token>` 헤더를 사용합니다.

이 방식으로 모바일, 데스크톱, Render 재시작 상황에서도 공연 기록 생성과 수정이 안정적으로 유지됩니다.

## API 요약

### 인증

- `POST /api/auth/request-code`
- `POST /api/auth/verify-code`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `POST /api/auth/logout`

### 공연 기록

- `GET /api/concerts`
- `POST /api/concerts`
- `PUT /api/concerts/:id`
- `DELETE /api/concerts/:id`
- `GET /api/concerts/calendar/my`
- `POST /api/concerts/:id/add-to-calendar`
- `POST /api/concerts/:id/remove-from-calendar`
- `GET /api/concerts/statistics/my`

### 외부 데이터

- `GET /api/kopis/search` - KOPIS, 서울 열린데이터광장, 공공데이터포털 통합 공연 검색
- `GET /api/kopis/performance/:id` - KOPIS 공연 상세 조회
- `GET /api/artists`
- `GET /api/venues`

## 운영 메모

- 첫 방문 안내 팝업은 브라우저 `localStorage`의 `fesnote-welcome-seen` 값으로 제어됩니다.
- KOPIS, 서울 열린데이터광장, 공공데이터포털에서 가져온 공연 정보는 출연진, 장소, 가격이 부정확할 수 있어 사용자가 수정할 수 있습니다.
- 이메일 발송에 실패하면 Render 로그와 화면에 임시 인증번호가 표시됩니다.
- `.env`, `SESSION_SECRET`, `JWT_SECRET`, API 키는 커밋하지 않습니다.

## 라이선스

MIT

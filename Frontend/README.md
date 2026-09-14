# 도서 관리 시스템

> KT AIVLE School AI 트랙 미니프로젝트 5차 (Frontend)

<img src="https://github.com/user-attachments/assets/c4527184-1e44-4688-a68f-12df8db1f4b9">

## 프로젝트 소개

- 누구나 작가가 되어 자유롭게 글을 집필하고 공개할 수 있는 창작 플랫폼입니다.
- 회원가입/로그인 후 도서를 등록·수정하고, 다른 작가를 팔로우하며, 댓글과 평점으로 소통할 수 있습니다.
- 작가의 감성과 이야기가 그대로 반영될 수 있도록 AI 표지 생성 기능을 지원합니다.

미니프로젝트 4차의 json-server 목업 버전을 기반으로, 실제 Spring Boot 백엔드(`../BackEnd`)와 통신하도록 전환하고 인증·팔로우·댓글 기능을 추가한 버전입니다.

<br>

## 시스템 아키텍처

```mermaid
graph LR
 User(("사용자"))
 Client["FrontEnd<br>(React + Vite)"]
 Server["BackEnd<br>(Spring Boot)"]
 AI["OpenAI API"]

 User -- "UI 조작" --> Client
 Client -- "REST API<br>(JWT 인증)" --> Server
 Client -- "AI 표지 생성 요청" --> AI
 AI -- "이미지 데이터(base64) 반환" --> Client
```

<br>

## 주요 기능

### 회원 / 인증
- 회원가입, 로그인, 로그아웃 (JWT 기반)
- 이메일·닉네임 중복 확인

### 도서
- 도서 등록·수정·삭제, 상세 조회, 조회수 집계
- 제목/작가/장르/출판사/가격대 등 상세 검색, 장르별 카테고리 필터링
- 조회수 기준 인기 랭킹, 출판일 기준 신작 랭킹

### AI 표지 생성
- 스타일·배경·조명·타이포그래피 태그 선택 및 프롬프트 입력으로 표지 생성
- 1회 생성에 최대 3가지 샘플 제공, 등록 후에도 언제든 재생성 가능

### 소셜
- 작가 프로필 페이지, 팔로우 / 언팔로우
- 도서별 댓글 작성과 평점(1~5) 등록
- 마이페이지에서 내가 등록한 도서, 즐겨찾기, 팔로우 목록 확인

<br>

## 기술 스택

### Environment
<img src="https://img.shields.io/badge/VISUAL STUDIO CODE-181717?style=for-the-badge&logo=none&logoColor=white"> <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white"> <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">

### Development
<img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"> <img src="https://img.shields.io/badge/react-61DAFB?style=for-the-badge&logo=react&logoColor=black"> <img src="https://img.shields.io/badge/vite-9135FF?style=for-the-badge&logo=vite&logoColor=black"> <img src="https://img.shields.io/badge/mui-007FFF?style=for-the-badge&logo=mui&logoColor=white"> <img src="https://img.shields.io/badge/react router-CA4245?style=for-the-badge&logo=reactrouter&logoColor=white"> <img src="https://img.shields.io/badge/OpenAI API-412991?style=for-the-badge&logo=openai&logoColor=white">

### Communication
<img src="https://img.shields.io/badge/figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white"> <img src="https://img.shields.io/badge/notion-000000?style=for-the-badge&logo=notion&logoColor=white"> <img src="https://img.shields.io/badge/zoom-0B5CFF?style=for-the-badge&logo=zoom&logoColor=white"> <img src="https://img.shields.io/badge/Microsoft Teams-6264A7?style=for-the-badge&logo=microsoftteams&logoColor=white">

<br>

## 프로젝트 구조

```text
Frontend/
├── public/                  # 정적 파일 (파비콘, 아이콘 등)
├── src/
│   ├── assets/               # 이미지 및 UI 에셋
│   ├── context/
│   │   └── AuthContext.jsx   # 로그인 상태 전역 관리
│   ├── components/
│   │   ├── auth/              # 로그인, 회원가입
│   │   ├── common/            # Header, 상세 검색 패널
│   │   ├── detail/             # 도서 상세 정보
│   │   ├── edit/               # 도서 등록/수정, AI 표지 에디터
│   │   ├── list/                # 도서 목록, 마이페이지
│   │   ├── main/                # 메인 화면, 검색바
│   │   └── pages/               # Home, 작가 프로필 페이지
│   ├── util/
│   │   └── bookCoverService.js  # AI 표지 생성 API 연동
│   ├── App.jsx               # 라우터
│   └── main.jsx               # React 진입점
└── .env                      # 환경 변수 (VITE_API_BASE_URL, VITE_OPENAI_API_KEY)
```

<br>

## 설치 및 실행

### 사전 요구사항
- Node.js / npm
- 실행 중인 백엔드 서버 (`../BackEnd` 참고)

### 환경 변수

프로젝트 루트에 `.env` 파일 생성:
```
VITE_API_BASE_URL=http://localhost:8080
VITE_OPENAI_API_KEY=
```

### 실행

```sh
npm install
npm run dev
```

<br>

## 화면 구성

|메인 화면 |도서 목록 |
|--------|--------|
|<img src="https://github.com/user-attachments/assets/1a76f89e-b3c5-41f8-ae42-61477d71240d"> |<img width="1895" height="908" alt="image" src="https://github.com/user-attachments/assets/b334a398-0247-411b-9d68-c69d7ff44bc5" /> |
|도서 검색 기능과 도서 랭킹 제공 |사이드바에서 장르별 모아보기 기능 |
|신규 도서 등록|도서 표지 생성|
|<img src="https://github.com/user-attachments/assets/7ed3444e-996e-4ec5-8382-4563cf8dcd52"> |<img src="https://github.com/user-attachments/assets/0ee21aeb-7347-4635-9ddb-c01a070ca8ca" /> |
|제목, 저자, 내용 등 정보 입력 |태그와 프롬프트를 입력하여 원하는 AI 표지 생성 |
|도서 상세 정보|AI 표지 수정|
|<img src="https://github.com/user-attachments/assets/cdb48da5-fde7-403f-b94d-5a024bb54017"> |<img src="https://github.com/user-attachments/assets/96d6a1dd-b497-4d69-b95d-184b4b1c12a2"> |
|등록한 도서 정보 내용 출력 |표지 수정도 생성 시와 동일 |

<br>

## 팀원 및 R&R

| 이름 | 역할 | 담당 기능 |
|------|------|-----------|
| 박태정 | 조장 | PM·기획, AI/Frontend 연동 |
| 김다진 | PPT | 백엔드 개발 |
| 황민서 | 검토담당자 | 백엔드 개발 |
| 배수성 | 타임키퍼 | 백엔드 개발 |
| 유지은 | 발표자 | 백엔드 개발 |
| 이채은 | 서기 | AI/Frontend 연동 |
| 김다애 | PPT | 통합/예외 처리 |
| 김경민 | - | 예비군 훈련으로 대부분 불참, 백엔드 일부 참여 |

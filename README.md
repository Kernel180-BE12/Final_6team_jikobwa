# Final Project

## 기술 스택

### Frontend
- React
- TypeScript

### Backend
- Java (JDK21)
- Spring Boot (3.3.4)
- Spring Security
- JWT (0.11.5)

### Database
- PostgreSQL

### ORM/Mapping
- MyBatis (3.0.4)

### Cache/Session Management
- Redis
- Spring Session Data Redis

### Logging
- Log4j2 (2.22.1)
- log4j-slf4j2-impl

### Build Tool
- Gradle

### Development Convenience
- Lombok (1.18.30)
- Spring Boot Devtools
- Annotation/Configuration Processors

### Environment Settings
- UTF-8 encoding
- Java compile release 21

### Test
- Spring Boot Starter Test (JUnit Platform)
- Mockito
- Spring Security Test

## 프로젝트 구조

```
Final_Project/
├── backend/                        # Spring Boot 백엔드 프로젝트
│   ├── build.gradle                # Gradle 빌드 설정
│   ├── gradlew                     # Gradle Wrapper (Linux/Mac)
│   ├── gradlew.bat                 # Gradle Wrapper (Windows)
│   ├── gradle/
│   │   └── wrapper/
│   │       └── gradle-wrapper.properties
│   └── src/
│       └── main/
│           ├── java/
│           │   └── com/example/finalproject/
│           │       └── FinalProjectApplication.java
│           └── resources/
│               ├── application.yml  # Spring Boot 설정
│               └── log4j2.xml      # Log4j2 설정
├── frontend/                       # React 프론트엔드 프로젝트
│   ├── package.json                # React 의존성
│   ├── tsconfig.json               # TypeScript 설정
│   ├── public/
│   │   └── index.html
│   └── src/
│       ├── App.tsx
│       ├── index.tsx
│       ├── App.css
│       └── index.css
├── .gitignore
└── README.md
```

## 환경 설정

### 1. 환경 변수 설정
`.env` 파일을 생성하고 다음 내용을 추가하세요:

```env
# 데이터베이스 설정
DB_USERNAME=postgres
DB_PASSWORD=your_password_here

# Redis 설정
REDIS_PASSWORD=

# JWT 설정
JWT_SECRET=your-super-secret-jwt-key-here
```

### 2. 데이터베이스 설정
PostgreSQL 데이터베이스를 설치하고 `final_project` 데이터베이스를 생성하세요.

### 3. Redis 설정
Redis 서버를 설치하고 실행하세요.

## 실행 방법

### Backend 실행
```bash
cd backend
./gradlew bootRun
```

### Frontend 실행
```bash
cd frontend
npm install
npm start
```

## API 엔드포인트
- Backend: http://localhost:8080/api
- Frontend: http://localhost:3000

## API 테스트 (Postman)

### Postman 설치 및 설정

#### 1. Postman 설치
- [Postman 다운로드](https://www.postman.com/downloads/)
- 설치 후 실행

#### 2. 환경 변수 설정
Postman에서 새로운 Environment를 생성하고 다음 변수를 설정하세요:

```
Environment Variables:
- baseUrl: http://localhost:8080/api
- token: (로그인 후 받은 JWT 토큰)
```

#### 3. Collection 생성
1. Collections → New Collection 생성
2. Collection 레벨에서 기본 Headers 설정:
   ```
   Content-Type: application/json
   Accept: application/json
   ```

### 기본 API 테스트

#### 헬스체크
```
GET {{baseUrl}}/health
```

#### 로그인
```
POST {{baseUrl}}/auth/login
Headers:
  Content-Type: application/json
Body:
{
  "username": "test@example.com",
  "password": "password123"
}
```

#### 사용자 목록 조회
```
GET {{baseUrl}}/users
Headers:
  Authorization: Bearer {{token}}
```

### Postman 사용 팁

#### 1. 자동 토큰 저장
로그인 API의 Tests 탭에 다음 스크립트 추가:
```javascript
if (pm.response.code === 200) {
    const response = pm.response.json();
    pm.environment.set("token", response.token);
}
```

#### 2. 요청 자동화
- Collection Runner를 사용하여 여러 API를 순차적으로 테스트
- Pre-request Scripts로 공통 로직 처리
- Tests Scripts로 응답 검증 자동화

#### 3. 환경별 설정
- Development: `baseUrl: http://localhost:8080/api`
- Production: `baseUrl: https://your-domain.com/api`

### 대안 도구

#### Thunder Client (VS Code 확장)
- VS Code 확장 마켓플레이스에서 "Thunder Client" 검색
- 설치 후 Ctrl+Shift+P → "Thunder Client: New Request"
- 빠른 API 테스트에 유용

# 청소년 활동 정보 MCP 서버

공공데이터포털의 청소년 활동 정보 API를 활용한 MCP (Model Context Protocol) 서버입니다.

## 개요

이 프로젝트는 여성가족부의 청소년 활동 정보 서비스를 MCP 프로토콜을 통해 Claude AI와 연동할 수 있도록 구현한 서버입니다. MCP SDK를 사용하여 처음부터 구현했으며, Tools, Resources, Prompts를 모두 제공합니다.

## 주요 기능

### 🔧 Tools (도구)

#### 청소년 활동 API 도구
1. **get_sido_list** - 시도(광역자치단체) 목록 조회
2. **get_sigungu_list** - 시군구(기초자치단체) 목록 조회
3. **search_youth_activities** - 청소년 활동 정보 검색
   - 지역별 검색 (시도, 시군구)
   - 키워드 검색
   - 페이징 지원

#### 유틸리티 도구
4. **echo** - 메시지 에코 (테스트용)
5. **get_time** - 현재 시간 조회

### 📦 Resources (리소스)

1. **youth://info** - 서버 정보
2. **youth://api-guide** - API 사용 가이드
3. **youth://sido-codes** - 시도 코드 참조표

### 💬 Prompts (프롬프트)

1. **search-guide** - 청소년 활동 검색 방법 안내
2. **region-guide** - 지역 코드 조회 방법 안내

## 설치 및 설정

### 1. 패키지 설치

```bash
npm install
```

### 2. API 키 발급

1. [공공데이터포털](https://www.data.go.kr/) 회원가입
2. 청소년 활동 정보 서비스 API 신청
3. 발급받은 서비스 키 확인

### 3. 환경 변수 설정

`.env` 파일을 생성하고 API 키를 설정합니다:

```bash
# .env.example을 복사하여 .env 파일 생성
cp .env.example .env
```

`.env` 파일 내용:
```
YOUTH_API_SERVICE_KEY=your_service_key_here
```

### 4. 빌드

```bash
npm run build
```

## 실행

### 직접 실행

```bash
npm start
```

### 개발 모드

```bash
npm run dev
```

## Claude Desktop에서 사용하기

Claude Desktop의 설정 파일(`claude_desktop_config.json`)에 다음을 추가하세요:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "youth-activity": {
      "command": "node",
      "args": ["/절대/경로/mcp-test/build/index.js"],
      "env": {
        "YOUTH_API_SERVICE_KEY": "your_service_key_here"
      }
    }
  }
}
```

또는 `.env` 파일을 사용하는 경우:

```json
{
  "mcpServers": {
    "youth-activity": {
      "command": "node",
      "args": ["/절대/경로/mcp-test/build/index.js"],
      "cwd": "/절대/경로/mcp-test"
    }
  }
}
```

## 사용 예시

Claude와 대화하면서 다음과 같이 활용할 수 있습니다:

```
사용자: 서울시의 청소년 봉사활동을 찾아줘

Claude: (get_sido_list로 서울시 코드 확인 후)
        (search_youth_activities를 사용하여 검색)
        서울시의 청소년 봉사활동 목록을 찾았습니다...
```

## 프로젝트 구조

```
mcp-test/
├── src/
│   ├── index.ts              # MCP 서버 메인 코드
│   └── youthApiClient.ts     # 청소년 활동 API 클라이언트
├── build/                    # 컴파일된 JavaScript 파일
├── .env.example              # 환경 변수 예시
├── package.json              # 프로젝트 설정
├── tsconfig.json             # TypeScript 설정
└── readme.md                 # 이 파일
```

## 기술 스택

- **TypeScript** - 타입 안전성
- **@modelcontextprotocol/sdk** - MCP 프로토콜 구현
- **axios** - HTTP 클라이언트
- **xml2js** - XML 파싱
- **dotenv** - 환경 변수 관리
- **Node.js** - 런타임 환경

## API 정보

- **데이터 제공**: 여성가족부
- **API 출처**: [공공데이터포털](https://www.data.go.kr/)
- **서비스명**: 청소년 활동 정보 서비스

## 라이선스

MIT

## 기여

이슈와 풀 리퀘스트를 환영합니다!

# Figma Make UI/UX 디자인 프롬프트 - QA Dashboard

**작성일**: 2025-11-18
**대상 시스템**: Bitbucket PR 데이터 기반 QA 관리 대시보드
**디자인 철학**: 심플하고 모던한 데이터 중심 UI/UX

---

## 📐 디자인 개요 (Design Brief)

### 프로젝트 목적
Bitbucket PR 데이터를 활용하여 QA 프로세스의 **지연을 조기에 식별**하고, **병목 지점을 시각화**하여 QA 매니저와 팀 리더가 신속하게 조치할 수 있도록 지원하는 실시간 관리 대시보드 UI/UX 디자인

### 핵심 비즈니스 가치
- 300일 이상 지연 PR 즉시 발견 (현재 4개 방치 중)
- QA 매니저 작업 시간 99% 단축 (30분 → 3초)
- 주간 리포트 작성 시간 95% 단축 (2시간 → 5분)
- 병목 지점 명확화로 프로세스 개선 ROI 300% 향상

---

## 🎯 UX 디자인 5단계 원칙 (Jesse James Garrett Framework)

### 1️⃣ Strategy (전략) - "왜 만드는가?"

#### 비즈니스 목표
1. **지연 PR 조기 발견**: 5일 이상 방치된 PR을 자동으로 탐지하여 즉시 알림
2. **병목 지점 시각화**: WAITING_FIRST_REVIEW 등 워크플로우 단계별 지연 원인 파악
3. **팀 성과 측정**: 개인별/그룹별 PR 처리 성과를 주/월/분기/년 단위로 집계
4. **실시간 모니터링**: 5분 주기 자동 갱신으로 최신 상태 유지
5. **의사결정 지원**: 데이터 기반 QA 프로세스 개선 방향 제시

#### 사용자 니즈
**Primary User: QA 매니저/리드**
- 문제: 수동으로 지연 PR 추적 → 30분 소요, 정확도 낮음
- 니즈: 3초 만에 전체 현황 파악, 긴급 조치 대상 즉시 식별
- 목표: 월요일 아침 체크 시간 99% 단축

**Secondary User: 개발 팀 리더**
- 문제: Excel로 주간 리포트 수동 작성 → 2시간 소요
- 니즈: 자동 리포트 생성, 트렌드 분석 차트
- 목표: 팀 성과 실시간 모니터링

**Tertiary User: 개별 개발자**
- 문제: 내 PR 상태 파악 어려움, 리뷰어에게 일일이 문의
- 니즈: 내 PR 필터링, 리뷰어 응답 시간 확인
- 목표: 병목 단계 알림 받기

#### 성공 지표
- **조기 발견율**: 지연 PR 발견 시간 30분 → 3초 (99.9% 개선)
- **리포트 생성**: 2시간 → 5분 (95% 개선)
- **사용자 만족도**: 베타 테스터 피드백 긍정 90% 이상
- **프로세스 개선**: 지연 PR 50% 감소, 평균 처리 시간 20% 단축

---

### 2️⃣ Scope (범위) - "무엇을 만드는가?"

#### 핵심 기능 (Must-Have)

**F1. 실시간 KPI 대시보드**
- 총 PR 수 (1,107개)
- 지연 PR 수 (5일 이상, 4개)
- 평균 처리 시간 (19.4일)
- 병합률 (97%)
- 각 KPI는 이전 대비 변화량 표시 (Delta 값)

**F2. 긴급 조치 필요 PR 테이블**
- 5일 이상 OPEN 상태 PR 목록
- 컬럼: 긴급도 🔴/🟡, PR ID, 제목, 작성자, 경과 시간, 현재 단계, 리뷰어
- 정렬: 경과 시간 내림차순 (391일 → 324일)
- 클릭: Bitbucket PR 페이지로 새 탭 열기

**F3. 기간별 집계 필터**
- 집계 단위 선택: 주별(Week) / 월별(Month) / 분기별(Quarter) / 연별(Year)
- 날짜 범위 선택기: 캘린더 UI
- ISO 주차 표시: 2024-W45, 2024-W46 등
- 분기 표시: 2024-Q1, 2024-Q2 등

**F4. 개인/그룹 집계 필터**
- 팀 선택: QA팀, 백엔드팀, 프론트엔드팀 등
- 개인 선택: 드롭다운 또는 자동완성 검색
- 비교 모드: 개인 vs 팀 평균 표시

**F5. PR 상태 분포 파이 차트**
- MERGED (96.9%) - 파란색 #2196F3
- OPEN (0.4%) - 주황색 #FFA500
- APPROVED (%) - 초록색 #4CAF50
- NEEDS_WORK (%) - 빨간색 #FF5722
- DECLINED (2.7%) - 회색 #9E9E9E

**F6. 병목 지점 막대 차트**
- X축: WAITING_FIRST_REVIEW, WAITING_AUTHOR_RESPONSE, WAITING_APPROVAL, WAITING_MERGE
- Y축: 평균 소요 시간 (시간 단위)
- 색상: 병목 지점(40% 이상) 빨강, 25-40% 주황, 25% 미만 초록
- 주요 병목 강조: WAITING_FIRST_REVIEW (100%, 빨강)

**F7. 리뷰어 성과 테이블**
- 컬럼: 리뷰어명, 평균 응답 시간, 완료율, 대기 PR 수, 평가(⭐), 상태
- 조건부 서식: 대기 PR ≥7개 → 빨강 배경 강조
- 상태: 🟢 정상 / 🔴 과부하

**F8. 탭 네비게이션**
- 📊 Overview (개요)
- 👥 Team Analysis (팀 분석)
- 📈 Trends (트렌드)
- 🔍 PR Details (PR 상세)

**F9. 자동 새로고침**
- 5분 주기 자동 갱신
- 마지막 업데이트 시간 표시: "2분 전"
- 수동 새로고침 버튼: 🔄

#### 부가 기능 (Nice-to-Have)

**F10. 고급 검색**
- 제목/설명/댓글 내용 검색
- 정규식 지원
- 검색 결과 하이라이트

**F11. Excel/PDF Export**
- 주간/월간 리포트 자동 생성
- 버튼: 📥 Export

**F12. Slack 알림 연동**
- 지연 PR 알림 (매일 09:00)
- SLA 위반 알림 (실시간)

---

### 3️⃣ Structure (구조) - "어떻게 동작하는가?"

#### 정보 아키텍처 (Information Architecture)

```
QA 관리 대시보드
├── 헤더 (Header)
│   ├── 로고 & 제목
│   ├── 마지막 업데이트 시간
│   └── 새로고침 버튼
│
├── 사이드바 필터 (Left Sidebar)
│   ├── 기간 선택
│   │   ├── 집계 단위: 주/월/분기/년 (라디오 버튼)
│   │   └── 날짜 범위: 캘린더 (Date Range Picker)
│   ├── 그룹 선택
│   │   ├── 팀 선택: 드롭다운 (QA팀, 백엔드팀, 전체)
│   │   └── 개인 선택: 자동완성 검색
│   └── 상태 필터
│       ├── OPEN (체크박스)
│       ├── MERGED (체크박스)
│       ├── DECLINED (체크박스)
│       └── 지연만 표시 (토글)
│
├── 메인 콘텐츠 (Main Content)
│   ├── KPI 카드 영역 (4개 카드 가로 배치)
│   │   ├── 총 PR
│   │   ├── 지연 PR
│   │   ├── 평균 처리 시간
│   │   └── 병합률
│   │
│   ├── 탭 네비게이션 (Tabs)
│   │   ├── 📊 Overview
│   │   ├── 👥 Team Analysis
│   │   ├── 📈 Trends
│   │   └── 🔍 PR Details
│   │
│   └── 탭 콘텐츠 (Tab Content)
│       │
│       ├── [Tab 1: Overview]
│       │   ├── 긴급 조치 필요 PR 테이블
│       │   ├── PR 상태 분포 파이 차트 (왼쪽)
│       │   └── 병목 지점 막대 차트 (오른쪽)
│       │
│       ├── [Tab 2: Team Analysis]
│       │   ├── 팀별 비교 막대 차트
│       │   ├── 팀 성과 테이블
│       │   └── 개인 vs 팀 평균 비교
│       │
│       ├── [Tab 3: Trends]
│       │   ├── 기간별 트렌드 라인 차트
│       │   ├── 주간/월간 통계 테이블
│       │   └── 증감율 분석
│       │
│       └── [Tab 4: PR Details]
│           ├── 전체 PR 목록 테이블 (정렬, 필터)
│           ├── 페이지네이션 (50개/페이지)
│           └── 상세 보기 모달
│
└── 푸터 (Footer)
    ├── 데이터 소스 정보
    └── 마지막 동기화 시간
```

#### 사용자 플로우 (User Flow)

**Flow 1: QA 매니저 월요일 아침 체크**
```
1. 대시보드 접속
   ↓
2. Overview 탭 자동 표시
   ↓
3. KPI 카드 확인 (지연 PR: 4개 🔴)
   ↓
4. 긴급 조치 필요 PR 테이블 확인
   ↓
5. PR ID 클릭 → Bitbucket 페이지 열기
   ↓
6. 리뷰어 재배정 조치
```

**Flow 2: 팀 리더 주간 리포트 작성**
```
1. 사이드바에서 기간 선택: 주별, 지난주
   ↓
2. Team Analysis 탭 선택
   ↓
3. 팀별 비교 차트 확인
   ↓
4. Export 버튼 클릭 → PDF 생성
   ↓
5. 리포트 메일 전송
```

**Flow 3: 개발자 본인 PR 확인**
```
1. 사이드바에서 개인 선택: 본인 이름
   ↓
2. PR Details 탭 선택
   ↓
3. 내 PR 목록 확인
   ↓
4. 병목 단계 확인 (WAITING_FIRST_REVIEW)
   ↓
5. 리뷰어에게 알림
```

#### 인터랙션 설계

**인터랙션 1: 필터 적용**
- 트리거: 사이드바 필터 변경
- 액션: 메인 콘텐츠 실시간 갱신 (<500ms)
- 피드백: 로딩 스피너 표시

**인터랙션 2: PR 클릭**
- 트리거: PR ID 클릭
- 액션: Bitbucket 페이지 새 탭 열기
- URL: https://bitbucket.ips.co.kr/projects/{project}/repos/{repo}/pull-requests/{id}

**인터랙션 3: KPI 카드 호버**
- 트리거: 마우스 오버
- 액션: 상세 툴팁 표시
- 내용: 이전 주 대비 변화량, 트렌드 미니 차트

**인터랙션 4: 자동 새로고침**
- 트리거: 5분 경과
- 액션: 백그라운드 데이터 갱신
- 피드백: "업데이트 중..." 배지

---

### 4️⃣ Skeleton (골격) - "어디에 배치하는가?"

#### 레이아웃 구조 (1920x1080 기준)

```
┌─────────────────────────────────────────────────────────────┐
│  HEADER (1920x80px)                                         │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ 🔍 QA 관리 대시보드  │  Last Update: 2분 전  │ 🔄    │   │
│  └──────────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  SIDEBAR (280px)                  MAIN CONTENT (1640px)     │
│  ┌──────────────────┐    ┌──────────────────────────────┐  │
│  │ 필터 설정        │    │ KPI CARDS (4개, 각 380px)    │  │
│  │                  │    │ ┌─────┐┌─────┐┌─────┐┌─────┐│  │
│  │ 📅 기간 선택     │    │ │총 PR││지연 ││평균 ││병합 ││  │
│  │  ○ 주별         │    │ │1,107││ 4개 ││19.4││ 97%││  │
│  │  ○ 월별         │    │ └─────┘└─────┘└─────┘└─────┘│  │
│  │  ○ 분기별       │    │                              │  │
│  │  ○ 연별         │    │ TABS                         │  │
│  │                  │    │ [Overview][Team][Trends][PR] │  │
│  │ 👥 그룹 선택     │    │                              │  │
│  │  [QA팀 ▼]       │    │ TAB CONTENT                  │  │
│  │                  │    │ ┌──────────────────────────┐│  │
│  │ 🔍 상태 필터     │    │ │🚨 긴급 조치 필요 PR      ││  │
│  │  ☑ OPEN         │    │ │                          ││  │
│  │  ☐ MERGED       │    │ │ (테이블 영역)            ││  │
│  │  ☐ DECLINED     │    │ └──────────────────────────┘│  │
│  │                  │    │                              │  │
│  │ ⚡ 지연만 표시    │    │ ┌────────────┐┌────────────┐│  │
│  │  [토글 ON]      │    │ │ 파이 차트  ││ 막대 차트  ││  │
│  │                  │    │ │            ││            ││  │
│  └──────────────────┘    │ │ (차트)     ││ (차트)     ││  │
│                           │ └────────────┘└────────────┘│  │
│  (높이: 1000px)          └──────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

#### 컴포넌트 상세 와이어프레임

**컴포넌트 1: KPI 카드 (380x140px 각)**

```
┌────────────────────────────────┐
│  🔴 지연 PR                    │  ← 아이콘 + 라벨 (16px)
│                                │
│         4개                    │  ← 메트릭 값 (48px, Bold)
│                                │
│      ▼ -2개 (vs 이전 주)      │  ← Delta 값 (14px, Red)
└────────────────────────────────┘
```

**컴포넌트 2: 긴급 조치 필요 PR 테이블 (1640x400px)**

```
┌─────────────────────────────────────────────────────────────────┐
│ 🚨 긴급 조치 필요 PR (5일 이상 지연)                             │
├────┬────┬───────────────┬────────┬─────────┬──────────┬────────┤
│긴급│PR  │제목           │작성자  │경과시간 │현재단계   │리뷰어  │
├────┼────┼───────────────┼────────┼─────────┼──────────┼────────┤
│🔴  │1234│[S03] API 성능 │윤민정  │391.8일  │첫리뷰대기│김철수  │
│🔴  │1235│[S03] 버그 수정│윤민정  │362.8일  │첫리뷰대기│이영희  │
│🔴  │1236│[S03] 기능 추가│윤민지  │334.9일  │첫리뷰대기│박민수  │
│🔴  │1237│[S03] 리팩토링 │손보희  │324.9일  │첫리뷰대기│정수연  │
└────┴────┴───────────────┴────────┴─────────┴──────────┴────────┘
```

**컴포넌트 3: PR 상태 분포 파이 차트 (800x400px)**

```
┌──────────────────────────────────┐
│  PR 상태 분포                    │
│                                  │
│       ╱─────╲                    │
│      │       │  MERGED (96.9%)  │
│      │   ●   │  OPEN (0.4%)     │
│      │       │  DECLINED (2.7%) │
│       ╲─────╱                    │
│                                  │
│  [범례: ■ MERGED  ■ OPEN  ■ ...] │
└──────────────────────────────────┘
```

**컴포넌트 4: 병목 지점 막대 차트 (800x400px)**

```
┌──────────────────────────────────┐
│  워크플로우 병목 지점             │
│                                  │
│  시간(h)                         │
│  25 ┤                            │
│  20 ┤  ███                       │
│  15 ┤  ███  ███                  │
│  10 ┤  ███  ███  ███             │
│   5 ┤  ███  ███  ███  ███        │
│   0 └──┴───┴───┴───┴───         │
│       첫    작성  승인  병합      │
│       리뷰  자응  대기  대기      │
│                                  │
│  ⚠️ 주요 병목: 첫 리뷰 대기      │
└──────────────────────────────────┘
```

**컴포넌트 5: 리뷰어 성과 테이블 (1640x300px)**

```
┌─────────────────────────────────────────────────────────────┐
│ 👥 리뷰어 성과 분석                                          │
├────────┬─────────┬────────┬────────┬──────┬─────────────┤
│리뷰어  │평균응답 │완료율  │대기 PR │평가  │상태         │
├────────┼─────────┼────────┼────────┼──────┼─────────────┤
│김철수  │2.1시간  │95.0%   │3개     │⭐⭐⭐│🟢 정상      │
│이영희  │4.8시간  │88.0%   │7개     │⭐⭐  │🔴 과부하    │ ← 빨강 배경
│박민수  │1.5시간  │98.0%   │2개     │⭐⭐⭐│🟢 정상      │
└────────┴─────────┴────────┴────────┴──────┴─────────────┘
```

---

### 5️⃣ Surface (표면) - "어떻게 보이는가?"

#### 디자인 시스템

**컬러 팔레트 (Color Palette)**

**Primary Colors (주요 색상)**
- Primary Blue: `#1976D2` - 헤더, 주요 버튼, 링크
- Secondary Teal: `#00897B` - 강조, 서브 액션

**Status Colors (상태 색상)**
- Success Green: `#4CAF50` - 정상 상태, 완료, 긍정 메트릭
- Warning Yellow: `#FFC107` - 주의 필요, 중간 상태
- Error Red: `#F44336` - 긴급, 위험, 부정 메트릭
- Info Blue: `#2196F3` - 정보, 안내

**Chart Colors (차트 색상)**
- MERGED: `#2196F3` (파란색)
- OPEN: `#FFA500` (주황색)
- APPROVED: `#4CAF50` (초록색)
- NEEDS_WORK: `#FF5722` (빨간색)
- DECLINED: `#9E9E9E` (회색)

**Neutral Colors (중립 색상)**
- Text Primary: `#212121` (90% 불투명)
- Text Secondary: `#757575` (60% 불투명)
- Background: `#FAFAFA` (매우 밝은 회색)
- Surface: `#FFFFFF` (흰색)
- Border: `#E0E0E0` (밝은 회색)

**타이포그래피 (Typography)**

**Font Family**
- Primary: 'Pretendard', 'Inter', -apple-system, sans-serif
- Monospace: 'JetBrains Mono', 'Fira Code', monospace (숫자, 코드)

**Font Sizes**
- H1 (페이지 제목): 28px, Bold, #212121
- H2 (섹션 제목): 24px, Semi-Bold, #212121
- H3 (컴포넌트 제목): 18px, Semi-Bold, #212121
- Body Large: 16px, Regular, #212121
- Body: 14px, Regular, #212121
- Caption: 12px, Regular, #757575
- Metric (KPI 값): 48px, Bold, #212121
- Delta (변화량): 14px, Medium, #4CAF50 or #F44336

**간격 및 여백 (Spacing)**

**Grid System**
- Container Max Width: 1920px
- Column Count: 12
- Gutter: 24px
- Margin: 32px (좌우)

**Component Spacing**
- Section Gap: 32px
- Component Gap: 24px
- Element Gap: 16px
- Inner Padding: 12px

**아이콘 (Icons)**

**Icon Library**
- Material Icons (Outlined style)
- Size: 24px (기본), 48px (큰 아이콘)
- Color: #757575 (기본), #1976D2 (액티브)

**주요 아이콘**
- 🔍 - 검색, 대시보드 로고
- 🔄 - 새로고침
- 📊 - Overview 탭
- 👥 - Team Analysis 탭
- 📈 - Trends 탭
- 🔍 - PR Details 탭
- 🚨 - 긴급 알림
- ⚠️ - 경고
- ✅ - 완료, 정상
- 🔴 - Critical 긴급도
- 🟡 - Warning 긴급도
- 🟢 - Normal 상태
- ⭐ - 평가 등급

**그림자 및 깊이 (Elevation)**

**Shadow Levels**
- Level 0 (Flat): box-shadow: none
- Level 1 (카드): box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24)
- Level 2 (호버): box-shadow: 0 3px 6px rgba(0,0,0,0.15), 0 2px 4px rgba(0,0,0,0.12)
- Level 3 (모달): box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23)

**둥근 모서리 (Border Radius)**
- Small: 4px (버튼, 입력 필드)
- Medium: 8px (카드, 컴포넌트)
- Large: 12px (모달, 팝업)
- Circle: 50% (아바타, 아이콘 버튼)

#### UI 스타일 가이드

**KPI 카드 스타일**
```css
.kpi-card {
  width: 380px;
  height: 140px;
  background: #FFFFFF;
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
  padding: 20px;
  transition: box-shadow 0.3s ease;
}

.kpi-card:hover {
  box-shadow: 0 3px 6px rgba(0,0,0,0.15), 0 2px 4px rgba(0,0,0,0.12);
}

.kpi-icon {
  font-size: 24px;
  margin-bottom: 8px;
}

.kpi-value {
  font-size: 48px;
  font-weight: 700;
  color: #212121;
  line-height: 1;
}

.kpi-delta {
  font-size: 14px;
  font-weight: 500;
  margin-top: 8px;
}

.kpi-delta.positive { color: #4CAF50; }
.kpi-delta.negative { color: #F44336; }
```

**테이블 스타일**
```css
.data-table {
  width: 100%;
  background: #FFFFFF;
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.12);
  overflow: hidden;
}

.data-table th {
  background: #FAFAFA;
  font-size: 14px;
  font-weight: 600;
  color: #757575;
  text-align: left;
  padding: 16px;
  border-bottom: 1px solid #E0E0E0;
}

.data-table td {
  font-size: 14px;
  color: #212121;
  padding: 16px;
  border-bottom: 1px solid #F5F5F5;
}

.data-table tr:hover {
  background: #FAFAFA;
}

.data-table tr.critical {
  background: #FFEBEE;
}

.data-table tr.warning {
  background: #FFF3E0;
}
```

**버튼 스타일**
```css
.button-primary {
  background: #1976D2;
  color: #FFFFFF;
  font-size: 14px;
  font-weight: 500;
  padding: 10px 24px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
  transition: background 0.3s ease;
}

.button-primary:hover {
  background: #1565C0;
}

.button-secondary {
  background: #FFFFFF;
  color: #1976D2;
  border: 1px solid #1976D2;
}

.icon-button {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: #FFFFFF;
  border: 1px solid #E0E0E0;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
```

**차트 스타일 가이드**

**파이 차트**
- 크기: 800x400px
- 범례 위치: 오른쪽
- 애니메이션: Fade-in, 1초
- 호버 효과: 섹션 강조, 툴팁 표시

**막대 차트**
- 크기: 800x400px
- 바 너비: 60px
- 바 간격: 40px
- 애니메이션: Bottom-up, 1초
- 호버 효과: 바 강조, 정확한 값 툴팁

**라인 차트**
- 크기: 1640x400px
- 선 두께: 2px
- 포인트 크기: 6px
- 그리드: 10% 불투명도
- 애니메이션: Left-to-right, 1.5초

#### 반응형 디자인 (Responsive Design)

**Breakpoints**
- Desktop Large: ≥1920px (기본)
- Desktop: 1440-1919px (사이드바 260px)
- Laptop: 1024-1439px (사이드바 숨김, 토글)
- Tablet: 768-1023px (KPI 2열, 차트 1열)
- Mobile: ≤767px (KPI 1열, 테이블 스크롤)

**모바일 최적화**
- 사이드바: 하단 시트 (Bottom Sheet)
- KPI 카드: 1열 세로 배치
- 테이블: 가로 스크롤
- 차트: 세로 배치, 높이 300px

---

## 🎨 Figma Make 구현 가이드

### 프레임 구조 (Frames)

**1. 메인 프레임**
- Name: "QA Dashboard - Desktop"
- Size: 1920 x 1080px
- Background: #FAFAFA

**2. 헤더 프레임**
- Name: "Header"
- Size: 1920 x 80px
- Position: X=0, Y=0
- Background: #1976D2
- 컴포넌트:
  - 로고 + 제목 (왼쪽 정렬, X=32, Y=24)
  - 업데이트 시간 (오른쪽 정렬, X=1740, Y=28)
  - 새로고침 버튼 (오른쪽 정렬, X=1860, Y=20)

**3. 사이드바 프레임**
- Name: "Sidebar"
- Size: 280 x 1000px
- Position: X=0, Y=80
- Background: #FFFFFF
- Shadow: Level 1
- 컴포넌트:
  - 기간 선택 섹션 (Y=20)
  - 그룹 선택 섹션 (Y=200)
  - 상태 필터 섹션 (Y=360)

**4. KPI 카드 프레임 (4개)**
- Name: "KPI Card - Total PRs" / "Delayed PRs" / "Avg Time" / "Merge Rate"
- Size: 380 x 140px
- Position: X=312/716/1120/1524, Y=100
- Background: #FFFFFF
- Shadow: Level 1
- Auto Layout: Vertical, Gap=8px, Padding=20px

**5. 탭 네비게이션 프레임**
- Name: "Tab Navigation"
- Size: 1640 x 56px
- Position: X=280, Y=260
- Background: #FFFFFF
- Border Bottom: 1px solid #E0E0E0
- 컴포넌트: 4개 탭 버튼 (Auto Layout Horizontal, Gap=0)

**6. 탭 콘텐츠 프레임 (Overview)**
- Name: "Tab Content - Overview"
- Size: 1640 x 724px
- Position: X=280, Y=316
- Background: Transparent
- 컴포넌트:
  - 긴급 PR 테이블 (Y=0, Height=400px)
  - 파이 차트 (Y=432, X=0, 800x292px)
  - 막대 차트 (Y=432, X=840, 800x292px)

### 컴포넌트 (Components)

**컴포넌트 1: KPI Card**
- Variants: 4개 (Total, Delayed, AvgTime, MergeRate)
- Properties:
  - Icon (Component Instance)
  - Label (Text, 14px, #757575)
  - Value (Text, 48px Bold, #212121)
  - Delta (Text, 14px Medium, #4CAF50 or #F44336)
- States: Default, Hover

**컴포넌트 2: Table Row**
- Variants: 3개 (Normal, Critical, Warning)
- Properties:
  - Urgency Icon (Component)
  - PR ID (Text, 14px, #1976D2, Underline)
  - Title (Text, 14px, #212121)
  - Author (Text, 14px, #212121)
  - Age (Text, 14px, #F44336)
  - Stage (Text, 14px, #757575)
  - Reviewers (Text, 14px, #757575)
- States: Default, Hover, Selected

**컴포넌트 3: Tab Button**
- Variants: 4개 (Overview, Team, Trends, PRDetails)
- Properties:
  - Icon (Component)
  - Label (Text, 14px, #757575 or #1976D2)
- States: Default, Active, Hover

**컴포넌트 4: Filter Section**
- Properties:
  - Title (Text, 12px, #757575)
  - Options (Auto Layout Vertical)
- Types:
  - Radio Group (기간 선택)
  - Dropdown (그룹 선택)
  - Checkbox Group (상태 필터)
  - Toggle (지연만 표시)

### 인터랙션 (Interactions)

**인터랙션 1: KPI 카드 호버**
- Trigger: Mouse Enter
- Action: Change to "Hover" variant
- Transition: Smart Animate, 200ms

**인터랙션 2: 탭 클릭**
- Trigger: On Click
- Action: Change to corresponding tab content frame
- Transition: Dissolve, 300ms

**인터랙션 3: PR ID 클릭**
- Trigger: On Click
- Action: Open URL (https://bitbucket.ips.co.kr/...)
- Transition: None

**인터랙션 4: 새로고침 버튼**
- Trigger: On Click
- Action: Rotate 360deg
- Transition: Spring, 500ms

### Auto Layout 설정

**헤더**
- Direction: Horizontal
- Alignment: Space Between
- Padding: 24px (좌우), 20px (상하)
- Gap: 16px

**사이드바**
- Direction: Vertical
- Alignment: Top Left
- Padding: 24px
- Gap: 32px (섹션 간)

**KPI 카드 컨테이너**
- Direction: Horizontal
- Alignment: Top Left
- Padding: 0
- Gap: 24px

**테이블**
- Direction: Vertical
- Alignment: Top Left
- Padding: 0
- Gap: 0 (행 간)

---

## 📝 Figma Make 프롬프트 템플릿

### 프롬프트 예시

```
Create a modern, clean QA management dashboard UI design for Bitbucket PR monitoring.

DESIGN SYSTEM:
- Style: Minimal, data-driven, professional
- Color Palette:
  * Primary: #1976D2 (Blue)
  * Success: #4CAF50 (Green)
  * Warning: #FFC107 (Yellow)
  * Error: #F44336 (Red)
  * Background: #FAFAFA (Light Gray)
  * Surface: #FFFFFF (White)
- Typography:
  * Font: Pretendard, Inter, sans-serif
  * H1: 28px Bold
  * Body: 14px Regular
  * Metric: 48px Bold
- Spacing: 24px grid system
- Shadows: Subtle elevation (0 1px 3px rgba(0,0,0,0.12))
- Border Radius: 8px for cards

LAYOUT (1920x1080px):
1. Header (Full Width, 80px)
   - Logo & Title: "🔍 QA 관리 대시보드" (Left)
   - Last Update: "2분 전" (Right)
   - Refresh Button: 🔄 (Right)

2. Sidebar (280px, Left)
   - Section 1: Period Filter
     * Radio Buttons: 주별/월별/분기별/연별
     * Date Range Picker
   - Section 2: Group Filter
     * Team Dropdown
     * Person Search
   - Section 3: Status Filter
     * Checkboxes: OPEN, MERGED, DECLINED
     * Toggle: Show Delayed Only

3. Main Content (1640px, Right)
   - KPI Cards Row (4 cards, 380x140px each):
     * Card 1: Total PRs (1,107개)
     * Card 2: Delayed PRs (4개, Red)
     * Card 3: Avg Time (19.4일)
     * Card 4: Merge Rate (97%)
   - Each card includes:
     * Icon (24px)
     * Label (14px, Gray)
     * Value (48px Bold, Black)
     * Delta (14px, Green/Red, ▼-2개)

   - Tab Navigation:
     * 📊 Overview (Active)
     * 👥 Team Analysis
     * 📈 Trends
     * 🔍 PR Details

   - Tab Content (Overview):
     A. Urgent PR Table (1640x400px)
        - Title: "🚨 긴급 조치 필요 PR (5일 이상 지연)"
        - Columns: Urgency, PR ID, Title, Author, Age, Stage, Reviewers
        - Rows: 4 rows with red background
        - Sample Data:
          * 🔴 #1234 "[S03] API 성능 개선" 윤민정 391.8일 첫리뷰대기 김철수
          * 🔴 #1235 "[S03] 버그 수정" 윤민정 362.8일 첫리뷰대기 이영희

     B. Charts Row (2 charts side by side):
        - Left: Pie Chart (800x400px)
          * Title: "PR 상태 분포"
          * Segments:
            - MERGED: 96.9% (Blue #2196F3)
            - OPEN: 0.4% (Orange #FFA500)
            - DECLINED: 2.7% (Gray #9E9E9E)

        - Right: Bar Chart (800x400px)
          * Title: "워크플로우 병목 지점"
          * Bars:
            - WAITING_FIRST_REVIEW: 18.5시간 (Red #F44336)
            - WAITING_AUTHOR_RESPONSE: 12.3시간 (Orange #FFA500)
            - WAITING_APPROVAL: 6.5시간 (Green #4CAF50)
            - WAITING_MERGE: 3.6시간 (Green #4CAF50)
          * Warning Label: "⚠️ 주요 병목: 첫 리뷰 대기"

COMPONENTS TO CREATE:
1. KPI Card Component
   - Variants: Total, Delayed, AvgTime, MergeRate
   - States: Default, Hover
   - Auto Layout: Vertical, Gap 8px, Padding 20px

2. Table Row Component
   - Variants: Normal, Critical, Warning
   - States: Default, Hover, Selected
   - Background: White (Normal), #FFEBEE (Critical), #FFF3E0 (Warning)

3. Tab Button Component
   - Variants: Overview, Team, Trends, PRDetails
   - States: Default, Active, Hover
   - Active: Blue underline, Bold text

4. Chart Component
   - Types: Pie, Bar, Line
   - Animated: Yes
   - Responsive: Yes

INTERACTIONS:
- KPI Cards: Hover effect (elevation shadow)
- Tab Buttons: Click to switch content (dissolve 300ms)
- PR IDs: Clickable links (underline on hover)
- Refresh Button: Rotate 360deg on click

RESPONSIVE DESIGN:
- Desktop: 1920px (4 KPI cards per row)
- Laptop: 1440px (sidebar collapsible)
- Tablet: 1024px (2 KPI cards per row)
- Mobile: 768px (1 KPI card per row, horizontal scroll tables)

STYLE EMPHASIS:
- Clean, minimal design
- Data-first approach
- High contrast for readability
- Color-coded urgency (Red/Yellow/Green)
- Professional, trustworthy appearance
- Accessible for color-blind users

OUTPUT FORMAT:
- Figma file with organized layers
- Components library
- Design system documentation
- Interactive prototype
```

---

## 🎯 디자인 목표 체크리스트

### 사용성 (Usability)
- [ ] 3초 내에 지연 PR 수 파악 가능
- [ ] 5초 내에 병목 지점 식별 가능
- [ ] 클릭 3회 이내로 모든 정보 접근
- [ ] 모바일에서도 핵심 정보 확인 가능

### 가독성 (Readability)
- [ ] 텍스트 대비율 4.5:1 이상 (WCAG AA)
- [ ] 숫자 및 메트릭 한눈에 인식 가능
- [ ] 색상 코딩으로 긴급도 즉시 파악
- [ ] 테이블 행 스캔 용이성

### 일관성 (Consistency)
- [ ] 동일한 컴포넌트 재사용
- [ ] 통일된 컬러 팔레트
- [ ] 일관된 간격 및 정렬
- [ ] 예측 가능한 인터랙션

### 접근성 (Accessibility)
- [ ] 색맹 사용자 고려 (아이콘 병행)
- [ ] 키보드 네비게이션 지원
- [ ] 스크린 리더 호환
- [ ] 충분한 터치 타겟 크기 (44x44px)

### 성능 (Performance)
- [ ] 로딩 스피너 명확
- [ ] 실시간 업데이트 피드백
- [ ] 차트 애니메이션 부드러움
- [ ] 반응 시간 < 300ms

---

## 📚 참고 자료

### 디자인 영감
- [Grafana Dashboard](https://grafana.com/) - 데이터 시각화
- [Datadog Monitoring](https://www.datadoghq.com/) - 실시간 대시보드
- [Linear Issue Tracker](https://linear.app/) - 모던 UI
- [GitHub Insights](https://github.com/features/insights) - PR 분석

### 컴포넌트 라이브러리
- Material Design 3
- Ant Design
- Tailwind UI

### 아이콘
- Material Icons (https://fonts.google.com/icons)
- Heroicons (https://heroicons.com/)

---

**작성 완료**: 2025-11-18
**다음 단계**: Figma Make에 프롬프트 입력 및 디자인 생성
**예상 효과**: 개발 전 UI/UX 검증으로 재작업 시간 70% 단축

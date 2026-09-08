# 🚜 자율주행 지게차(Autonomous Forklift) 디지털 트윈 & KPI 관제 시스템

> 물류 및 제조 현장에 투입되는 자율주행 지게차(AMR Forklift / AGV)의 핵심 성능 지표(KPI)를 실시간으로 추적·검증하고, 3D 디지털 트윈 환경에서 자율주행 및 팔레트 핸들링 작업을 제어할 수 있는 올인원 시뮬레이션 & 관제 플랫폼입니다.

---

## 🎯 6대 핵심 KPI 체계

| 지표명 | 목표값 (Target) | 설명 |
| :--- | :--- | :--- |
| **1. 충돌 사고율 (Safety)** | **0 건 (Zero Collision)** | LiDAR 기반 3단계 안전 존(Safe / Warning / Emergency) 및 동적 장애물 감지 |
| **2. 경로 추종 정밀도 (Precision)** | **±20 mm 이내** | 계획 궤적 대비 실제 지게차 중심 편차 실시간 RMSE(제곱평균제곱근) 계산 |
| **3. 팔레트 도킹 성공률 (Handling)** | **99.5% 이상** | 정밀 정렬 -> 포크 인입 -> 승강(Lift) -> 적재 7단계 상태 머신 기반 |
| **4. 시간당 처리량 (Throughput)** | **25 Pallets / hour** | 입고 -> 랙 적재 -> 출고 전체 사이클 타임(Cycle Time) 측정 |
| **5. 설비 종합 효율 (OEE)** | **95.0% 이상** | 총 운영 시간 대비 순수 작업 가동 시간 비율 |
| **6. 배터리 관리 효율 (Energy)** | **SOC ≤ 20% 시 자동 충전** | 잔여 배터리 모니터링 및 충전 베이(Charging Bay) 자동 복귀 |

---

## 🚀 빠른 시작 가이드 (Getting Started)

### 방법 1: 브라우저로 바로 실행 (Zero Config)
`index.html` 파일을 크롬(Chrome)이나 엣지(Edge) 브라우저에서 직접 열거나, VS Code Live Server 등을 통해 즉시 실행할 수 있습니다. (Three.js CDN 자동 연동)

### 방법 2: Vite 개발 서버로 실행
```bash
# 1. 의존성 설치
npm install

# 2. 로컬 개발 서버 실행
npm run dev

# 3. 브라우저에서 http://localhost:3000 접속
```

---

## 🖥️ 주요 기능 및 사용자 인터페이스

1. **3D 디지털 트윈 뷰포트 (Three.js WebGL)**
   - 스마트 보관 랙, 입고/출고/보관 구역, 자동 충전소 완비
   - 270도 가상 LiDAR 레이캐스팅 & 실시간 포인트 클라우드 시각화
   - 바퀴 조향, 마스트 포크 승강 및 팔레트 적재 물리 애니메이션

2. **카메라 뷰 모드**
   - **🌐 3D 자유 궤도**: 마우스 드래그로 360도 자유 회전 및 휠 줌인/아웃
   - **🎥 차량 추적 시점**: 이동하는 지게차를 후방 3인칭 시점으로 실시간 팔로우
   - **🗺️ 2D 탑다운 맵**: 창고 전체를 한눈에 볼 수 있는 2D 관제 맵 뷰

3. **작업 미션 발주 (FMS) & 연속 자율 모드**
   - 입고 구역 A/B, 보관 랙 1/2/3, 출고 구역 1/2 간 팔레트 이송 작업 발주
   - **연속 자율 미션 모드**: 지게차가 자동으로 최적 미션을 순환 수행하며 KPI 데이터 누적

4. **비상 안전 관제 (E-Stop)**
   - 긴급 정지 버튼 클릭 시 즉각적인 제동 및 OEE 다운타임 기록, 안전 복구 기능

---

## 📂 프로젝트 폴더 구조

```
d:/AI_Native/
├── index.html                 # 메인 웹 대시보드 & 3D 뷰포트
├── package.json               # 패키지 설정
├── vite.config.js             # Vite 설정
├── docs/
│   └── PROJECT_KPI.md         # 상세 KPI 정의서 및 공식/운영 표준서
├── src/
│   ├── main.js                # 앱 진입점 및 렌더 루프
│   ├── style.css              # 프리미엄 다크 테마 & 관제 UI 스타일
│   ├── config/
│   │   └── kpi_config.js      # KPI 목표치 및 창고 맵 좌표 설정
│   ├── simulation/
│   │   ├── WarehouseWorld.js  # 3D 물류창고 환경 및 장애물
│   │   ├── ForkliftModel.js   # 3D 지게차 기구학 및 승강 모델
│   │   ├── SensorSystem.js    # LiDAR 레이캐스팅 & 3-Zone 안전 판정
│   │   ├── NavigationEngine.js# 웨이포인트 주행 & 궤적 오차(mm) 계산
│   │   └── StateMachine.js    # 7단계 팔레트 핸들링 상태 머신
│   ├── controllers/
│   │   ├── KPITracker.js      # 실시간 KPI 집계 및 통계 엔진
│   │   └── MissionManager.js  # 작업 미션 큐 및 경로 생성기
│   └── ui/
│       ├── DashboardUI.js     # 실시간 지표 및 텔레메트리 바인딩
│       ├── MissionControlUI.js# 미션 발주 및 비상 정지 버튼 제어
│       └── TelemetryCharts.js # 실시간 오차 곡선 캔버스 차트
└── README.md
```

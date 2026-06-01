# Village Overpass Rush

밝은 마을과 고가도로를 배경으로 한 독자 제작 3D 아케이드 카트 레이싱 게임입니다. 로컬 브라우저에서 바로 실행하는 것을 목표로 만들었고, 드리프트로 부스터를 모아 쓰는 빠른 주행 리듬에 초점을 맞췄습니다.

## 실행 방법

1. 이 폴더의 `index.html`을 브라우저로 엽니다.
2. 카운트다운 후 바로 주행할 수 있습니다.

Three.js 로딩 방식:

- `index.html`은 먼저 `vendor/three.min.js`를 찾습니다.
- 해당 파일이 있으면 인터넷 없이 실행됩니다.
- 없으면 CDN `https://cdnjs.cloudflare.com/ajax/libs/three.js/0.148.0/three.min.js`로 자동 대체합니다.

완전 오프라인 실행을 원하면 Three.js 파일을 `vendor/three.min.js`로 넣어두면 됩니다.

## 조작법

| 키 | 기능 |
| --- | --- |
| `W` 또는 `↑` | 가속 |
| `S` 또는 `↓` | 감속 / 후진 |
| `A/D` 또는 `←/→` | 조향 |
| `Shift` | 드리프트 |
| `Ctrl` | 미니부스터 또는 보유 부스터 사용 |
| `R` | 주행 중 체크포인트 복귀, 완주 후 재시작 |
| `Sound On/Off` | 사운드 토글 |

## 부스터 시스템

- 드리프트를 유지하면 `MINI` 게이지가 차오릅니다.
- `MINI` 게이지가 충분할 때 `Ctrl`을 누르면 짧은 미니부스터가 발동됩니다.
- 드리프트를 잘 유지하면 `BOOST` 게이지가 차오르고, 가득 차면 부스터 슬롯이 1개 생깁니다.
- 부스터 슬롯은 최대 2개까지 보유할 수 있습니다.
- `Ctrl`을 누르면 보유 부스터를 1개 소비해서 일정 시간 자동 부스터가 지속됩니다.

## 구현 기능

- 3랩 레이스
- 순서 기반 체크포인트 판정
- 랩, 현재 시간, 베스트 랩, 최고 기록 저장
- 플레이어 빨간 스포츠 카트
- 같은 모델의 노란색 AI 라이벌 카트
- AI 직선 구간 부스터 사용
- 드리프트 연기, 스키드 마크, 차체 기울기
- 충돌 스파크, 화면 플래시, 카메라 흔들림
- 부스터 패드
- 1~8 코스 구간 표식
- 파란 주행 방향 화살표
- 헤어핀 경고 표식
- 고가도로, 기둥, 방음벽, 가드레일, 배너, 광고판, 마을 건물, 가로등, 나무, 구름, 산 배경
- 자연스러운 레이어형 Web Audio 엔진음, 바람소리, 부스터음, 충돌음
- 미니맵과 다음 체크포인트 표시

## 맵 흐름

`Village Overpass Rush`는 다음 흐름의 폐곡선 트랙입니다.

출발/도착 직선 -> 넓은 첫 우회전 -> 고가 진입 오르막 -> 고가도로 직선 -> 연속 S자 구간 -> 내리막 하강 -> 헤어핀 좌회전 -> 빌리지 구간 -> 마지막 직선

## 튜닝 위치

주요 값은 [src/game.js](./src/game.js) 상단 `CONFIG`에서 조절합니다.

- `player.turnRate`: 기본 조향 회전력
- `player.steerRise`: 조향 입력이 차오르는 속도
- `player.highSpeedSteerDamping`: 고속 조향 둔화 정도
- `player.driftGrip`: 드리프트 중 횡그립
- `player.driftChargeRate`: 미니부스터 충전 속도
- `player.boostBuildRate`: 드리프트로 부스터 슬롯을 채우는 속도
- `player.boostSlotSeconds`: 보유 부스터 1개의 지속 시간
- `player.boostAccel`: 부스터 가속력
- `ai.straightSpeed`, `ai.cornerSpeed`, `ai.boostSpeed`: AI 속도
- `roadWidth`: 트랙 폭

## 파일 구조

```text
.
├── index.html
├── style.css
├── src/
│   └── game.js
├── vendor/
│   └── README.md
└── assets/
```

## 점검 목록

- `index.html` 실행
- 카트 주행
- 드리프트
- 미니부스터
- 보유 부스터 슬롯 사용
- 3랩 완주
- 체크포인트 순서 판정
- AI 주행
- 순위 표시
- 타이머와 최고 기록 저장
- `R` 체크포인트 복귀 / 재시작

# Heat Check-In

NYC behavioral-health care teams를 위한 폭염 대응 연락 목록과 후속 조치 도구.

## 현재 상태

기존 공개 데이터 + 명시적인 합성 대상자 기반 로컬 인터랙티브 데모 구현. 외부 배포·실제 환자 데이터·EHR 연결 없음.
지도와 연락 목록 50:50, 대상자 선택 시 오른쪽 Call card 전환.

## 화면

실행 없이 먼저 화면만 보고 싶다면:

| Home | Team workspace / Call list |
|---|---|
| ![Home](references/04-redesign-home.png) | ![Workspace](references/05-redesign-workspace.png) |

(지도 패널은 OpenStreetMap iframe이라 인터넷 없이 캡처하면 위 스크린샷처럼 빈 칸으로 보일 수 있음 — 실제 브라우저에서 열면 지도가 뜸.)

## 실행

**필요한 것:** Python 3.9+ 만 있으면 됨. 별도 패키지 설치(`pip install`) 없음 — 표준 라이브러리만 사용.

```bash
git clone https://github.com/Hye-Seung-Kim/heat-check-in.git
cd heat-check-in
python3 -m http.server 8765 --bind 127.0.0.1 --directory dist
```

브라우저에서 http://127.0.0.1:8765/ 열기.

`dist/data/demo.json`은 이미 빌드되어 저장소에 커밋돼 있어서 위 두 줄이면 바로 뜬다. `scripts/prepare_data.py`는
합성 대상자·HVI 스냅샷을 **재생성**하고 싶을 때만 돌리면 됨(예: 시나리오를 바꾸거나 `docs/06-data-contract.md`
형식의 대상자 JSON을 새로 넣고 싶을 때):

```bash
python3 scripts/prepare_data.py                 # 기본 12명 합성 대상자로 재생성
python3 scripts/prepare_data.py --clients my_clients.json   # 직접 만든 대상자 목록으로 교체
```

소스 CSV(`data-sources/`에 캐시된 스냅샷)만 읽고 인터넷 접근 없이 동작한다. 지도 iframe과 구글 폰트만 인터넷이 필요하고,
그 외 데이터·폰트 폴백은 전부 로컬에서 뜬다.

실제 공개 HVI 4개 NTA, 역사적 2024년 ED 관측 153일, 명시적인 합성 대상자 12명 사용.
지도는 OpenStreetMap 지역 개요이며 HVI polygon layer는 아님.
편집 내용은 브라우저 localStorage에 저장. 시나리오 기준일은 2026-09-19로 고정.

### 빠르게 훑어보려면

1. 홈에서 **Open team call sheet** 클릭
2. **Simulate advisory**로 가상 폭염 경보 발효
3. `Contact first` 그룹의 대상자 하나 열어서 Call card 확인 (Why flagged / Known / Unknown / 적응형 질문)
4. Claim → 통화 결과 저장 → Follow-up 탭에서 담당자·상태 갱신
5. **Reset demo**로 초기화 (브라우저별 localStorage라 다른 브라우저/시크릿창에서는 항상 초기 상태)

## 구현

Home, call sheet, simulated advisory, 개인 근거·지역 맥락 분리, Claim, 동의 확인, 적응형 질문, 통화 결과, 재시도 task, 담당자·기한 수정, 지원 검증, 브라우저 저장, 초기화, 인쇄.

## 제한

Guide는 정적 안내. LLM 연결·임의 가중치 score·calibrated confidence·공식 대상자 adapter·실시간 경보는 미구현. Decision table은 합성 데모용이며 clinician 검토 전. top-K는 그룹별 표시 개수이고 자동 서비스 제외가 아님.
최신 사용자 제공 개요를 기준으로 SMI/SUD 대상, social worker/care team 사용자, Heat Check-In 명칭을 적용합니다.

## 문서

- [프로젝트 개요](docs/01-project-brief.md)
- [사용자 흐름 및 결정할 사항](docs/02-user-flow.md)
- [페이지 구성과 디자인 방향](docs/03-page-spec.md)
- [구현 범위와 인수 기준](docs/04-build-plan.md)
- [현재 보유 데이터 활용 계획](docs/05-existing-data-plan.md)
- [대상자 데이터 교체 계약](docs/06-data-contract.md)
- [사용자 제공 원문](references/original-proposal.txt)

`references/01~03`은 초기 디자인 단계에서 사용자가 제공한 외부 시각적 참고 자료(Pharos 제품)이며, 우리 제품 화면이 아니다.
Pharos 브랜드, 영국 임상 모델, 위험 수치는 제품 데이터로 사용하지 않는다. `references/04~05`가 실제 현재 화면 스크린샷이다.

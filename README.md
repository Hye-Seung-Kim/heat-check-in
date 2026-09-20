# Heat Check-In

NYC behavioral-health care teams를 위한 폭염 대응 연락 목록과 후속 조치 도구.

## 현재 상태

기존 공개 데이터 + 임시 합성 대상자 기반 로컬 인터랙티브 데모 구현. 외부 배포·실제 환자 데이터·EHR 연결 없음.
지도와 연락 목록 50:50, 대상자 선택 시 오른쪽 Call card 전환.

## 실행

이 폴더에서 `python3 scripts/prepare_data.py` 후 `python3 -m http.server 8765 --bind 127.0.0.1 --directory dist`.
브라우저에서 http://127.0.0.1:8765/ 열기.

실제 공개 HVI 4개 NTA, 역사적 2024년 ED 관측 153일, 명시적인 합성 대상자 12명 사용.
지도는 OpenStreetMap 지역 개요이며 HVI polygon layer는 아님. 지도와 웹폰트는 인터넷 필요; 그 외 로컬 데이터와 기본 폰트로 동작.
편집 내용은 브라우저 localStorage에 저장. 시나리오 기준일은 2026-09-19로 고정.

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

references의 세 이미지는 사용자가 제공한 시각적 참고 자료입니다. Pharos 브랜드, 영국 임상 모델, 위험 수치는 제품 데이터로 사용하지 않습니다.

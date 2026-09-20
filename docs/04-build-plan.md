# 구현 범위 및 인수 기준

## 단계 1 — 흐름 합의 (현재)

연락 목록/지도 비중과 바로 구현할지 확인. 문서와 참고 이미지는 이 폴더에 보관.

## 단계 2 — 작동하는 데모

- Home + call-sheet workspace + client panel + follow-up + guide.
- 명시적인 synthetic fixtures와 simulate advisory.
- Claim, adaptive questions, outcome logging, task assignment, retry, support verification.
- 데모 저장 방식을 문서화: 브라우저 로컬 저장 또는 서버 저장을 실제 구현에 맞게 표시.
- Reset demo로 원래 데이터 복원 가능.
- 데이터에서 그룹 수량 계산; 화면마다 임의 숫자 사용하지 않음.

## 단계 3 — 실제 데이터 연결

공식 schema 및 제공 범위를 확인한 뒤 adapter 작성. NWS/HVI 등은 해당 repository skill의 Search trigger를 읽고 접근·제약을 검증. 아직 live query를 수행하거나 실데이터 연결 완료를 주장하지 않음.

## MVP에서 보류

- 임의 가중치 기반 clinical risk score 및 근거 없는 confidence percentage.
- 실제 SMS/email/call 발신.
- 환자 데이터 및 실제 인증·EHR 연결.
- 미검증 임상 decision table.
- 실시간 자원 수용력 보장.

## 주요 인수 기준

1. Simulated event임이 모든 관련 화면에 표시된다.
2. 세 그룹의 수량과 목록이 일치한다.
3. 확인된 최신 답변은 반복 질문에서 빠지고 수정은 가능하다.
4. Unreachable은 목록에 남고 retry/escalation을 가진다.
5. Task accepted만으로 plan confirmed가 되지 않는다.
6. 모든 필수 지원 확인 후에만 완료 그룹으로 이동한다.
7. 새 필요를 기록하면 완료된 계획도 다시 review된다.
8. Consent unknown/no에서 일반 outreach 진행 대신 review 상태가 보인다.
9. 지도 맥락과 개인 사실이 구분된다.
10. 새로고침·초기화·키보드·좁은 화면 동작을 확인한다.

## 결과물 상태 표기

구현 이후 README에 실제 실행 방법, 검증 결과, mock/live 구분, 미구현 사항을 업데이트한다. 문서의 제안은 기능 구현 완료를 의미하지 않는다.

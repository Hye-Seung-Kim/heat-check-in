# 사용자 흐름 — 협의용 초안

## 사용자 확정 사항

1. 작업 화면: 지도와 연락 목록을 반반 배치.
2. 진행 방식: 사용자 흐름부터 함께 확정한 뒤 구현.

## 다음 협의 사항

대상자를 선택하면 왼쪽 지도를 유지하고 오른쪽 목록을 통화 카드로 전환하는 안을 제안. 지도는 팀 담당 지역과 냉방 자원 맥락을 표시하며, 개인 주소 핀은 기본에서 제외. Call card의 Back to list로 기존 목록·필터·스크롤을 복원.

## 추천 메인 흐름

소개 페이지 → Open call sheet → 담당 팀의 폭염 연락 목록 → 대상자 선택 → Claim → 연락 허용 여부 확인 → 통화 질문 → 결과 기록 → 후속 조치 배정 → 지원 확인 → 다음 폭염에서 갱신된 정보 사용.

### 1. 진입

- 발표용 진입: Landing의 Open call sheet.
- 실무용 진입: 전달받은 링크로 해당 팀·이벤트 목록에 직접 접근.
- 초기 데모는 고정된 synthetic team. 실제 로그인 및 메시지 전송을 구현했다고 표시하지 않음.

### 2. 폭염 이벤트

- Simulate advisory 버튼으로 데모 시작.
- 배너에 지역, 시작/종료, 정보 갱신 시각과 Simulated 표시.
- 실제 API 연결이 추가되더라도 데모 이벤트와 live 이벤트 구분.
- 비활성 상태에서도 기본 caseload 및 readiness 확인 가능.

### 3. 연락 목록

- 기본 탭: Unresolved needs / Needs verification / Plan confirmed.
- 각 행: synthetic ID, 주요 이유, 마지막 확인, 연락 상태, 담당자.
- top-K는 오늘의 처리 분량이며 나머지 사람을 숨기거나 제외하지 않음.
- 연락이 어려운 사람은 자동 후순위로 밀지 않고 retry/escalation 표시.
- 각 그룹의 수는 실제 데모 데이터에서 계산.

### 4. 대상자 카드와 Claim

- 대상자를 열면 Known / Needs verification / Why this client appears를 구분.
- Claim하면 In progress와 담당자가 표시됨.
- 이미 다른 팀원이 담당 중이면 중복 연락 대신 담당자와 상태 확인.
- 연락 동의가 No/Unknown이면 승인된 조직 절차를 확인할 review 상태. 데모에서 실제 발신 없음.

### 5. 적응형 통화 카드

질문 풀:
1. 현재 이용할 수 있는 냉방이 있나요?
2. 비용이나 고장 때문에 사용하기 어렵나요?
3. 대신 머물 수 있는 시원한 장소가 있나요?
4. 그곳에 가는 데 교통 지원이 필요한가요?
5. 담당 의료진에게 전달할 질문이 있나요?
6. 다음 연락 방법과 연락처를 확인할 수 있나요?

- 최근 확인된 항목은 요약해 보여주고 다시 묻지 않음.
- 오래됐거나 상황이 바뀐 항목은 재확인.
- 기존 답변도 수정 가능.
- 임상 질문의 내용은 기록·전달하며 자동 의료 조언은 하지 않음.

### 6. 결과 분기

**Reached, no open need:** 필수 정보가 확인되고 기존 필요도 해결되면 Plan confirmed.

**Reached, support needed:** 필요별 task 초안 → 사용자 검토 → owner와 due date 지정 → Open.

**Unreachable:** 실패 사유·시각 기록 → 재시도 일정 또는 supervisor escalation. 계획을 완료 처리하지 않음.

**Declined:** 거절 및 선호를 기록하고 수동 review. 지원 완료로 처리하지 않음.

**Consent unclear:** contact permission review로 이동.

### 7. 실제 지원 확인

Task: Open → Accepted → In progress → Support verified.
예외: Blocked / Cancelled with reason. 취소를 해결로 계산하지 않음.

- 교통 예약이나 수리 접수는 실제 필요 해결과 구분.
- 자원이 없으면 Blocked 및 대안·supervisor review 유지.
- 모든 필수 필요가 해결되고 계획이 유효할 때만 Plan confirmed.

### 8. 다음 이벤트

- 기존 답변·출처·확인일을 유지.
- 현재 유효한 답변은 반복 질문을 줄임.
- 변경 사항, 새 필요, 유효기간 경과가 있으면 재확인 목록으로 복귀.
- 중복 알림 억제는 새로운 필요를 막지 않음.

## 데모 시나리오

Simulate advisory → 3개 그룹 확인 → cooling unknown 대상자 열기 → Claim → 냉방 고장·교통 필요 기록 → 두 task 배정 → 다른 대상자 Unreachable 기록 → retry 생성 → 지원 확인 후 첫 대상자 Plan confirmed → 다음 이벤트에서 저장된 답변 표시.

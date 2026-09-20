# 페이지 구성과 디자인 방향

## 시각 방향

사용자 참고 이미지의 넉넉한 여백, 얇은 경계선, 흰색·따뜻한 회색 배경, 검정 primary button, 절제된 amber 강조를 적용.
참고 이미지의 어두운 영상 오버레이와 재생 버튼은 복제하지 않음.
화면 문구는 영어, 기획 문서는 한국어 중심.

## 1. Home

- Header: Heat Check-In / How it works / Open call sheet.
- Eyebrow: NYC · Behavioral health care teams.
- Headline: Know who to check on before the heat arrives.
- Description: An explained outreach list, focused questions, and a clear next action for your care team.
- CTA: Open call sheet.
- 세 설명 카드: Prioritize outreach / Ask what is missing / Follow through.
- 실제 사용자는 직접 workspace로 들어갈 수 있도록 함.

## 2. Call-sheet workspace

- 상단: 팀 이름, event 상태, Simulate advisory.
- 이벤트 배너: 기간·영향 지역·source timestamp·simulated/live 구분.
- 세 그룹 탭과 수량.
- 왼쪽 50%: 팀 담당 지역·자원 맥락 지도.
- 오른쪽 50%: 대상자 연락 목록. 대상자 선택 시 같은 영역이 통화 카드로 전환되는 안을 제안.
- 주요 액션: Open card, Claim, Print call sheet.
- Print는 필요한 최소 정보만 출력하며 담당자·출력일·synthetic 표시 포함.

지도와 연락 목록의 50:50 배치는 사용자 확정 사항. 지도는 개인 위험 점수의 시각화로 쓰지 않음. 실제 client 주소를 표시하지 않으며 데모 위치는 명확한 합성/지역 맥락으로 표시.

## 3. Client call card — 오른쪽 상세 패널

- Synthetic client ID, priority group, owner.
- Why flagged / Known / Unknown or stale.
- Consent and preferred contact.
- Adaptive questions and note.
- Outcome: Reached / Unreachable / Declined.
- Save check-in → 검토 가능한 action draft.
- Close 또는 Back to list.

## 4. Follow-up view — workspace 내부 탭

- 필요, 대상자, 담당 역할, 마감, 상태.
- 필터: Open / Blocked / Verified.
- 지원 확인 시 기록자·시각·확인 근거 저장.
- 미배정·기한 경과·연락 실패를 supervisor가 확인.

## 5. Guide — 참고 이미지의 보조 패널

- workspace에서 열고 닫는 오른쪽 패널.
- 추천 질문: Why is this client listed? / What is still unknown? / What happens after an unsuccessful call?
- 실제 AI 연결 전에는 scripted demo guide로 명시.
- 현재 client facts와 workflow 설명으로 범위 제한.
- Guide가 call card의 주요 행동을 가리지 않도록 한 번에 하나의 패널을 우선 표시.

## 공통 상태

- No advisory: readiness 목록 유지.
- No matching clients: 영향을 받는 caseload 없음 표시.
- All confirmed: 다음 검토 필요 시점 안내, 전체 목록 유지.
- Data unavailable: 정보 없음 표시, 안전함으로 해석하지 않음.
- Save failure: 입력 보존 및 재시도.
- Mobile: 목록 우선, 지도는 별도 탭, 상세는 전체 화면.
- 접근성: 색상과 텍스트를 함께 사용, 키보드 이동, 패널 포커스 복귀, label이 있는 입력.

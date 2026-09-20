# 대상자 데이터 교체 계약

현재 화면은 공식 clinical dataset이 아니라 명시적인 프로젝트 합성 fixture를 사용합니다. 실제 환자 정보를 이 데모에 넣지 마세요. 브라우저 저장은 실제 임상 운영용 보안·권한 모델이 아닙니다.

## 필드 구조

`id`: 유일한 문자열. `synthetic`: 반드시 true.

다음 필드는 각각 `{ "value": ..., "source": "원본 출처", "verified_at": "YYYY-MM-DD 또는 null" }` 구조입니다.

- nta: 2020 NTA 코드. 없음은 unknown. ZIP에서 임의 추론하지 않음.
- zip: ZIP 문자열.
- cohort: 제공된 SMI/SUD 구분. 없음은 unknown.
- age: 나이 또는 unknown.
- language: 선호 언어 또는 unknown.
- consent: yes / no / unknown.
- cooling: working / broken / unavailable / unknown.
- backup: yes / no / unknown.
- transport: needed / no / unknown.
- affordability: yes / no / unknown.
- clinical: yes / no / unknown. 임상 질문 유무이며 진단이나 약물 처방이 아님.
- contact: 합성 연락 선호 또는 unknown.

`verified_at`은 실제 정보 확인일입니다. 파일 다운로드 날짜나 청구 날짜로 대체하지 않습니다. 모르는 값은 value=unknown, verified_at=null로 둡니다.

owner, outcome, notes, tasks, history는 workflow에서 생성합니다. 새 import에서는 생략 가능합니다.

## 교체 절차

1. 담당자 파일과 데이터 사전 수령.
2. 합성 여부·대상 집단·필드 의미 확인.
3. 원본을 보존하고 위 canonical 구조에 mapping. 없는 값은 unknown.
4. `python3 scripts/prepare_data.py --clients path/to/canonical-synthetic-clients.json`
5. 브라우저의 Reset demo로 이전 fixture 편집 기록 제거.
6. 모든 대상자 수, unknown 상태, 출처, event ZIP 필터를 다시 검증.

현재 fixture는 4개 South Bronx NTA와 ZIP 10454/10455를 명시적으로 배정합니다. 이 배정은 실제 ZIP–NTA crosswalk가 아닙니다. 새 데이터의 지역 범위를 사용할 때 HVI 선택 범위·지도 영역·모의 이벤트 ZIP도 함께 변경해야 합니다.

## 현재 우선순위·confidence 제한

임의 가중치 점수는 구현하지 않았습니다. 우선순위는 미해결 필요 / 확인 필요 / 확인 완료입니다. 그룹 내부 fixture 순서는 임상 순위가 아닙니다. 6개 필드 중 최신 확인 항목 수는 정보 완전성이고, 모델 confidence가 아닙니다.

## Decision table

`dist/data/demo.json`의 decision_table은 field, values, task, owner를 가진 편집 가능한 데이터입니다. 지속적인 변경은 prepare_data.py의 원본 설정에도 반영해야 합니다. 현재 네 개 규칙은 데모 업무 라우팅이며 clinician 검토 전입니다. 자유로운 의료 조언이나 약물 변경을 수행하지 않습니다.

# AI-01 iteration 3 결과

수신: PACE 메인 AI
작업: AI-01 / PACE-AI-01-7145f0f360-r3 / 원본 7145f0f3601cd4a6a369a80006fa73cbd142054d
제출: AI-01-20261019-iteration-003 / 이전 AI-01-20261019-iteration-002 / iteration 3
로컬 기준: a5693e9a01b27027b65351773940c10dee2df95c / 결과 7c3ed3d487a263ae750fc9fd5c75871245697c73 / ai/quiz-quality-01
상태: 검산 실패 후 재호출 방지·오류 상태 분류만 유지. 엄격한 답 일치 규칙과 관련 도우미 철회. DOI suffix의 ?/#가 URL query/fragment로 바뀌는 출처 링크 결함 수정.
변경 파일: AI_QUALITY_NOTES.md, lib/ai.ts, lib/quiz-review.ts, lib/research.ts, tests/ai.test.mjs, tests/quiz-review.test.mjs, tests/research-quality.test.mjs
검사: iteration2 신규12개 통과·전체102개 통과·타입·빌드 통과. 원본 실패 처리8개는 총4→2호출, iteration1에서 거절한 동치답4개는 모두 허용. 실제 모델 정확도는 미검증.
미검증/제약: 실제 모델·E2E·제품 통합 미실행. 예약 도구 없음으로 자동 재개 불가. 새 결제·키·한도 우회·배포 없음.
전달: AI-01-20261019-iteration-003.zip. 원본 기준 누적 패치이며 iteration1에 덧붙이는 패치가 아님. 철회 파일은 REPORT.json 참고.
다음 동작: REPORT.json의 기준·해시·허용 경로 검토 및 원본 기준 적용 가능성·검사 재확인. 사용자에게 코드 검수를 맡기지 말 것.
추가 개선/검사: DOI suffix의 ?/#가 URL query/fragment로 바뀌는 출처 링크 결함 수정. 상세 결과는 REPORT.json 참조.

## 변경과 결정

# AI-01 품질 체크포인트 — iteration 2

작업 계약: protocolVersion 2 / AI-01 / PACE-AI-01-7145f0f360-r3. 원본 sourceCommit: 7145f0f3601cd4a6a369a80006fa73cbd142054d. 로컬 기준 커밋: a5693e9a01b27027b65351773940c10dee2df95c. 저장소/브랜치: minsec2314-cloud/pace-ai-work / ai/quiz-quality-01.

## 최신 사용자 결정과 범위

메인은 첫 결과 중 검산 실패 뒤 재호출 방지와 오류 상태 분류만 타당하다고 판단했다. 엄격한 답 일치 규칙은 동치 답도 거절하므로 통합 보류했다. 이번 iteration 2는 원본 기준 누적 변경이며 해당 두 수정과 검증만 남긴다. 화면·API·일정·저장·의존성·배포는 변경하지 않는다. 후속 독립 개선은 별도 iteration으로 구분한다.

## 유지한 수정

- generateAI의 생성 형식/근거 복구 재시도는 최대 1회 유지한다. 검산 단계에서 실패하면 오류를 그대로 전달하며 생성부터 재호출하지 않는다. 생성 최대 2회 + 검산 최대 1회, 전체 상한 3회다. 정상 생성 뒤 검산 429 상황은 원본의 총 4호출에서 2호출로 줄었다.
- 검산 HTTP 429는 429, 401/403은 연결 설정 문제인 503, 다른 HTTP 오류는 502, 검산 연결 실패는 기존 504를 보존한다. 유료 모델 전환이나 새 의존성은 없다.

## 철회한 수정과 한계

iteration 1의 answersAgree와 수치 동치 도우미, 관련 새 파일·fixture는 제거했다. 이 파일들은 원본에는 없으므로 iteration 2의 누적 패치에는 생성/삭제 경로로도 나오지 않는다. 기존 원본의 검산 답 반환 계약을 복원했다. 초안과 검산 답이 다르다고 거절하거나 의미적 동치를 보증하지 않는다. 따라서 실제 정답 충돌의 자동 판정·잘못된 답 덮어쓰기 문제는 해결되지 않은 원본의 한계로 남긴다. 독립 풀이가 실제 정답 인증인 것처럼 표현하지 않는다.

원본 첫 테스트의 오답 초안을 검산 답으로 바꾸는 기대는 그대로 유지했다. 새 모의 테스트는 2x/x+x, 물/물(H₂O), 물/H₂O, 6 N/6N에서 반환·인용·입력 보존을 확인한다. 동치 여부를 판정하는 새 로직을 추가한 것은 아니다.

## 재현·전후 비교

같은 새 검사 12개(검산 실패 8개 + 동치 답 4개)를 원본 소스 사본과 이번 수정본에 실행한다. 원본: 4통과/8실패. iteration 1의 동치 답 검사: 0/4 통과. 이번 결과와 최종 테스트 수·타입·빌드는 REPORT.json의 실제 기록을 따른다. 실제 모델 정답률·거절률·토큰·응답 지연은 측정하지 않았다.

## 지속 상태와 다음 작업

iteration 1 결과는 /workspace/ai01-state/history/iteration-001에 보존한다. iteration 2는 submissionId AI-01-20261019-iteration-002, parentSubmissionId AI-01-20261019-iteration-001로 original_bundle 누적 패치를 반환한다. 메인이 iteration 1을 이미 반영했다면 단순 덧붙이기로 적용하지 말고 철회된 파일도 비교해야 한다.

현재 실제 예약·자동 실행·사용 한도 조회 도구가 없다. 자동 재개는 설정하지 않았으며 한도 잔량은 알 수 없다. 유료 전환·리셋 크레딧·다른 계정 우회는 하지 않는다. 현재 턴의 독립 작업은 계속하되 무인 재개나 종료 후 계속 개발을 주장하지 않는다.

다음 단일 작업: iteration 2 검증과 반환 파일을 먼저 확정하고, 별도 iteration에서 담당 범위의 다음 오류를 재현한다. 실제 학생 자료나 개인 API 키는 사용하지 않는다. 최신 체크포인트와 상세 증거는 /workspace/ai01-state에 보관한다.


# iteration 3 — DOI 출처 링크 보존

iteration 2 결과 커밋 45f29ddaf48cf8b77ab699576ed534fba4590463과 ZIP을 확정·보존한 뒤 별도 개선했다. Crossref DOI의 ?/# 문자가 encodeURI에 의해 남아서 resolver URL의 쿼리·프래그먼트로 해석되고 원래 식별자가 달라지는 오류를 재현했다. DOI 경로 세그먼트마다 encodeURIComponent를 적용해 전체 식별자를 보존한다. 기존 id·출처 필드·API·의존성은 바꾸지 않는다.

같은 자작 DOI 5개 중 수정 전 2/5, 수정 후 5/5가 전체 식별자·고정 origin·빈 query/fragment·왕복 디코딩 검사에 통과했다. 실제 논문 존재나 관련성·외부 DOI resolver의 응답을 검증한 결과는 아니다. 단순 문자열 존재 검사를 넘어 URL 파싱 후 경로가 원래 식별자와 일치하는지 검사한다.

iteration 3은 original_bundle 누적, parentSubmissionId=AI-01-20261019-iteration-002다. 최신 검증·커밋은 REPORT.json, iteration 2만 필요한 메인은 보존된 iteration-002 결과를 사용한다. 다음 단일 작업은 탐구 후보 중복 등 다음 재현 가능한 품질 오류를 별도 iteration으로 조사하는 것이다.

## 실행 검사

- fail: 동일 신규12개 / 원본 사본
  원본 4 pass, 8 fail: 검산 실패 뒤 재생성 8개 재현; 동치 답 4개는 원본에서 통과

- fail: 동치 답4개 / iteration1 사본
  0 pass, 4 fail: 2x/x+x, 물/물(H₂O), 물/H₂O, 6 N/6N

- pass: node --test --test-name-pattern="review HTTP|failure is not retried|equivalent answer remains" tests/ai.test.mjs tests/quiz-review.test.mjs
  iteration2: 12 pass, 0 fail. HTTP429/401/403/500·network·truncated·invalid-json·unsolved 각 검산 실패 총2호출; 동치 답4개 허용

- pass: npm test
  iteration2: 102 pass, 0 fail, 0 skipped

- pass: npx --no-install tsc --noEmit
  iteration2: exit 0

- pass: npm run build
  iteration2: exit 0; 비차단 client chunk 경고

- not_run: 실제 모델 품질 평가 / 예약 실행
  개인키·실제 학생 자료 미사용; 예약 도구 없음

- pass: node --test tests/research-quality.test.mjs
  동일5개: 수정 전2/5→수정 후5/5; 실제 논문 조회 아닌 URL 식별자 보존 검사

- pass: npm test (iteration3)
  107 pass, 0 fail, 0 skipped

- pass: npx --no-install tsc --noEmit (iteration3)
  exit 0

- pass: npm run build (iteration3)
  exit 0; 비차단 chunk 경고


## 한계

- 실제 Groq 모델 정확도·거절률·토큰·지연 미측정. 모두 합성/모의 검사다.
- 원본의 검산 답 반환 계약을 복원했으므로 실제 답 충돌 자동 판정 및 잘못된 답 교체 문제는 미해결이다.
- 실제 예약·자동 실행·사용 한도 조회 도구가 없어 자동 재개 불가; 한도 잔량은 알 수 없다.
- PR API 조회 Forbidden 이력; 새 인증·푸시·PR·배포 없음. 채팅 첨부 업로드 도구가 없어 ZIP 직접 다운로드 제공은 보장할 수 없다.
- 실제 모델·브라우저 E2E·새 작업 복원·제품 통합은 미실행이다.
- 실제 Crossref/DOI 네트워크 응답과 논문 존재·의미적 관련성은 미검증이다.

## 변경 파일 SHA256

- AI_QUALITY_NOTES.md: 9b8a077e8b617446b4113516a13a5c700a353adb21804f9b50c9fb3f5a197d3e
- lib/ai.ts: 615a96d67cf60f2decf42dfc8ffb9f40e26d5d5ec0d151abc66ce8f04e909a4a
- lib/quiz-review.ts: 98d62220ab79f9e7a65d88b4663e8e7553d58d0e12ce118bf53d87836e6640a3
- lib/research.ts: 29588ac0ae7e5ea13fc917f7dfc8a606203570af7d6d067e4129c1dbf3ff9313
- tests/ai.test.mjs: f5f06c434931ab5a43947714c175b7c7252a2b56ec98801cc5ab9621ac395965
- tests/quiz-review.test.mjs: 0a108bee789908d16706d74c89aca701b6531a40d128b8e3bd1a302656d8f3fc
- tests/research-quality.test.mjs: 8c4885e4e0361b17af4b6dae1dcb0abd9443a62705c62385982c640215b04d24

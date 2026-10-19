# AI-01 iteration 7 결과

수신: PACE 메인 AI
작업: AI-01 / PACE-AI-01-7145f0f360-r3 / 원본 7145f0f3601cd4a6a369a80006fa73cbd142054d
제출: AI-01-20261019-iteration-007 / 이전 AI-01-20261019-iteration-006 / iteration 7
로컬 기준: a5693e9a01b27027b65351773940c10dee2df95c / 결과 4edb7b923ec66ff2e119a6dd6efb51d400c3a610 / ai/quiz-quality-01
상태: 검산 실패 후 재호출 방지·오류 상태 분류만 유지. 엄격한 답 일치 규칙과 관련 도우미 철회. DOI suffix의 ?/#가 URL query/fragment로 바뀌는 출처 링크 결함 수정. 동일 중심 질문의 탐구 후보 중복을 거절하고 기존 1회 복구 상한을 검증. 한국어 조사형 검색어의 관련 문단 누락을 낮은 가중치의 제한적 조사 제거형으로 보완. 잘못된 학술 검색 항목에서 정상 출처를 보존하고 깨진 응답 형식을 오류로 구분. 중복 자료ID의 기출/수업 근거 역할 우회를 모델 호출 전 차단.
변경 파일: AI_QUALITY_NOTES.md, lib/ai.ts, lib/quiz-review.ts, lib/research.ts, lib/topics.ts, tests/ai.test.mjs, tests/quiz-review.test.mjs, tests/research-quality.test.mjs, tests/topics.test.mjs
검사: iteration2 신규12개 통과·전체102개 통과·타입·빌드 통과. 원본 실패 처리8개는 총4→2호출, iteration1에서 거절한 동치답4개는 모두 허용. 실제 모델 정확도는 미검증.
미검증/제약: 실제 모델·E2E·제품 통합 미실행. 예약 도구 없음으로 자동 재개 불가. 새 결제·키·한도 우회·배포 없음.
전달: AI-01-20261019-iteration-007.zip. 원본 기준 누적 패치이며 iteration1에 덧붙이는 패치가 아님. 철회 파일은 REPORT.json 참고.
다음 동작: REPORT.json의 기준·해시·허용 경로 검토 및 원본 기준 적용 가능성·검사 재확인. 사용자에게 코드 검수를 맡기지 말 것.
추가 개선/검사: DOI suffix의 ?/#가 URL query/fragment로 바뀌는 출처 링크 결함 수정. 동일 중심 질문의 탐구 후보 중복을 거절하고 기존 1회 복구 상한을 검증. 한국어 조사형 검색어의 관련 문단 누락을 낮은 가중치의 제한적 조사 제거형으로 보완. 잘못된 학술 검색 항목에서 정상 출처를 보존하고 깨진 응답 형식을 오류로 구분. 중복 자료ID의 기출/수업 근거 역할 우회를 모델 호출 전 차단. 상세 결과는 REPORT.json 참조.

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


# iteration 4 — 탐구 후보의 동일 중심 질문 중복 거절

iteration 3 결과와 ZIP을 먼저 보존한 뒤 탐구 후보 3개가 완전히 같은 질문을 반복해도 통과하는 오류를 재현했다. topicSystem은 서로 다른 후보 3개를 요구하지만 readTopicIdeas는 항목별 형식과 개수만 검사했다. 이제 중심 질문의 앞뒤 및 연속 공백만 정규화해 정확히 중복된 질문은 거절한다. 제목·방법의 공통점이나 자연어 의미의 유사성으로 중복을 추측하지 않는다. 같은 제목/방법을 쓴 서로 다른 질문은 허용하는 대조 검사를 추가했다.

기존 유효 응답 fixture 중 같은 후보를 세 번 복제한 부분은 서로 다른 질문 3개로 바꿨다. 중복 탐지 없이 그 검사를 통과했다고 실제 주제 품질이 좋다고 주장하지 않는다. 중복 시 기존 형식 복구 1회로 서로 다른 후보를 반환하는 경로와 중복이 계속되면 2호출 뒤 502로 실패하는 경로를 검사했다. 새 동일4개 검사: 원본 1/4 통과, 수정 후 4/4 통과. 전체 자동 검사는 111개다. 실제 모델의 중복 발생률·제약 충족·탐구 실현 가능성 개선은 미측정이다.

iteration 4는 original_bundle 누적, parentSubmissionId=AI-01-20261019-iteration-003다. 각 회차 체크포인트와 ZIP은 별도로 보존하며 iteration 2의 분리된 전달본도 유지한다. 다음 단일 작업은 실제 답 충돌 처리의 요구를 메인과 조율하기 전, 과목 자료 검색의 관련 근거 누락을 새 합성 사례로 조사하는 것이다. 검증하지 않은 개선을 억지로 추가하거나 예약·사용 한도 상태를 꾸며 내지 않는다.


# iteration 5 — 한국어 조사 때문에 관련 문단을 놓치는 검색 오류

iteration 4를 먼저 확정·보관한 뒤, 미분계수는/극한의/운동량을 등의 질문에서 조사까지 포함한 문자열만 대조하여 관련 개념이 있는 페이지를 놓치는 오류를 재현했다. 기존 검색어는 그대로 두고, 한글 단어의 제한된 조사 제거형을 낮은 가중치(0.5)로 보강한다. 후보 원문·인용 내용·자료별 커버리지·예산·기출/수업 자료 역할은 바꾸지 않는다. 의미 검색이나 완전한 형태소 분석을 구현한 것은 아니다.

첫 7개 사례에 이어 별도 개념 3개와 짧은 명사 대조 2개를 추가했다. 최종 동일 검색 사례12개는 원본3/12→수정후12/12 통과다. 조사로 끝나는 명사 자체의 모호성, 혼합 영문·수식, 동의어 및 긴 실제 PDF 검색의 효과는 미검증이다. 실제 답변 정확도 개선 수치로 해석하지 않는다. 기존 정확한 검색어와 숫자, 짧은 사과/효과 명사를 보존하는 대조 검사를 포함했다. 전체 모의 테스트123개·타입·빌드 통과.

iteration 5는 original_bundle 누적, parentSubmissionId=AI-01-20261019-iteration-004다. iteration 2만 필요한 메인은 보존된 iteration-002 결과를 선택할 수 있다. 다음 단일 작업은 한국어 조사 보강의 모호한 명사·실제 형태 차이·다중 자료 순위 회귀를 추가 사례로 평가하는 것이다. 현재 계정의 잔량은 조회할 수 없고 한도 소진을 주장하지 않는다. 실제 예약이 없으므로 응답 종료 뒤 자동으로 개발이 이어진다고 말하지 않는다.


# iteration 6 — 부분적으로 잘못된 학술 검색 응답에서 정상 출처 보존

iteration 5 전달 ZIP은 GitHub 전달 전용 브랜치에 업로드하고 실제 HTTP 200·파일 SHA256까지 확인했다. 기본 브랜치·제품 소스 브랜치·배포를 변경하지 않았다. 메인이 자동 수신했다고 가정하지 않는다.

학술 검색 결과 한 항목이 null이거나 author 형식이 잘못되면 전체 목록 변환이 예외로 끝나는 오류, 배열이 아닌 title이 첫 글자로 잘려 출처 제목이 되는 오류, 마크업만 있는 빈 제목과 suffix 없는 DOI가 표시되는 오류를 재현했다. 정상 필수 항목만 변환하고 잘못된 선택 메타데이터는 저자 미확인으로 처리해 나머지 정상 출처를 보존한다. URL origin·DOI 인코딩·기존 Source 필드 계약은 유지한다.

API envelope 또는 JSON 자체가 잘못되면 성공한 빈 결과로 위장하지 않고 읽기 가능한 형식 오류를 전달한다. 동일 신규5개: 원본0/5→수정후5/5. DOI 포함 출처 검사10개·전체 모의128개·타입·빌드 통과. 이는 합성 응답의 변환/오류 경로 검사이며 실제 논문 존재·관련성·검색 정확도를 입증하지 않는다.

iteration 6은 original_bundle 누적, parentSubmissionId=AI-01-20261019-iteration-005다. 다음 단일 작업은 자료 ID가 중복될 때 기출 근거가 수업 자료 근거로 오인되는지 별도 재현하는 것이다.


# iteration 7 — 중복 자료 ID의 기출/수업 근거 혼동 차단

iteration 6 결과를 먼저 보관한 뒤, 기출과 수업 자료에 같은 materialId가 들어오면 기출 referenceId만 사용한 예상 문제도 수업 근거 검사를 통과하는 오류를 재현했다. citations는 materialId를 보관하므로 이 입력은 자료 역할과 원문 식별을 모호하게 만든다. generateAI 호출 초기에 중복 자료 ID를 400으로 거절하고 모델 호출을 0회로 유지한다. 같은 문장을 포함하더라도 ID가 다른 유효 자료는 거절하지 않는다. 일반 질문에서도 중복 자료 ID를 거절한다. 입력·출력 필드나 공통 API/상태·화면은 바꾸지 않는다.

동일 신규3개: 수정 전1/3→수정 후3/3. 기출/수업 역할 우회 재현, 일반 질문의 무의미한 모델 호출 차단, 서로 다른 ID의 같은 내용 허용 대조를 포함한다. 전체 모의131개·타입·빌드 통과. 실제 자료의 의미적 관련성이나 실제 모델 정답률을 검증한 결과는 아니다.

iteration 7은 original_bundle 누적, parentSubmissionId=AI-01-20261019-iteration-006다. 최신 코드 커밋·파일 해시·다음 재개 위치는 CHECKPOINT.json에 저장하고 각 ZIP을 전달 전용 GitHub 브랜치에 보존한다. iteration 2 단독 ZIP은 그대로 유지한다. 다음 단일 작업은 공백/대소문자/중복 페이지 등 자료 식별·인용 경계의 추가 실패 사례를 조사하는 것이다. 사용 한도 잔량은 조회 도구가 없어 알 수 없고, 실제 예약 도구가 없어 자동 재개가 불가능하다. 중단 후 계속 실행 중이라고 주장하지 않는다.

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

- fail: node --test --test-name-pattern="topic parser|duplicate topic questions" tests/topics.test.mjs (원본 비교)
  원본 1 pass, 3 fail; 동일 질문 3개가 그대로 통과하는 오류 재현

- pass: node --test tests/topics.test.mjs (iteration4)
  9 pass, 0 fail; 새4개 비교1/4→4/4; 중복 복구 최대2호출; 서로 다른 질문 대조군 유지

- pass: npm test (iteration4)
  111 pass, 0 fail, 0 skipped

- pass: npx --no-install tsc --noEmit (iteration4)
  exit 0

- pass: npm run build (iteration4)
  exit 0; 비차단 client chunk 경고

- fail: 조사형/정확어/신규 검색 사례12개 원본 비교
  원본3 pass,9 fail; 제한된 한 문단 예산에서 관련 페이지가 누락됨

- pass: node --test --test-name-pattern="Korean particle|particle expansion|new retrieval|short exact noun" tests/ai.test.mjs
  12 pass,0 fail; 첫7개와 추가5개; 검색 지표이며 실제 답 정확도 아님

- pass: npm test (iteration5)
  123 pass,0 fail,0 skipped

- pass: npx --no-install tsc --noEmit (iteration5)
  exit 0

- pass: npm run build (iteration5)
  exit 0; 비차단 client chunk 경고

- fail: 학술 응답 방어 신규5개 / 원본 비교
  0 pass,5 fail; null row·author·title·빈 DOI·잘못된 envelope/JSON 재현

- pass: node --test tests/research-quality.test.mjs (iteration6)
  10 pass,0 fail; 신규5개 모두 통과; 합성 응답

- pass: npm test (iteration6)
  128 pass,0 fail,0 skipped

- pass: npx --no-install tsc --noEmit (iteration6)
  exit 0

- pass: npm run build (iteration6)
  exit 0; 비차단 client chunk 경고

- fail: 중복자료ID 및 유효 대조3개 수정 전 재현
  1 pass,2 fail; 같은 materialId의 exam 인용만으로 lesson 근거 검사 우회

- pass: node --test --test-name-pattern="duplicate material IDs|distinct IDs" tests/ai.test.mjs
  3 pass,0 fail; 중복ID 요청은400·모델호출0; 서로 다른ID 동일내용 허용

- pass: npm test (iteration7)
  131 pass,0 fail,0 skipped

- pass: npx --no-install tsc --noEmit (iteration7)
  exit 0

- pass: npm run build (iteration7)
  exit 0; 비차단 client chunk 경고


## 한계

- 실제 Groq 모델 정확도·거절률·토큰·지연 미측정. 모두 합성/모의 검사다.
- 원본의 검산 답 반환 계약을 복원했으므로 실제 답 충돌 자동 판정 및 잘못된 답 교체 문제는 미해결이다.
- 실제 예약·자동 실행·사용 한도 조회 도구가 없어 자동 재개 불가; 한도 잔량은 알 수 없다.
- PR API 조회 Forbidden 이력; 새 인증·제품 소스 브랜치 푸시·PR·배포 없음. 결과 전달용 별도 브랜치로 ZIP을 제공하며 채팅 첨부 업로드 도구는 없다.
- 실제 모델·브라우저 E2E·새 작업 복원·제품 통합은 미실행이다.
- 실제 Crossref/DOI 네트워크 응답과 논문 존재·의미적 관련성은 미검증이다.
- 탐구 후보의 실제 의미적 중복·실행 가능성·실제 모델 응답 품질은 미측정이다.
- 조사 제거형은 제한적 어휘 보강이며 모호한 명사·혼합 영문/수식·동의어·실제 PDF 및 모델 정확도는 미검증이다.

## 변경 파일 SHA256

- AI_QUALITY_NOTES.md: dc55209c991ee39a2f2e00b7df74c8c6cea284887bdf904ccf5298bb60a8b257
- lib/ai.ts: 57c8ab37d7045e14d29843160e534a33055c507c6ee8f06907d9cddef21b1387
- lib/quiz-review.ts: 98d62220ab79f9e7a65d88b4663e8e7553d58d0e12ce118bf53d87836e6640a3
- lib/research.ts: e826ba85ef9fa654a1a568a0b590652cbfd1bdb96c0f7d73b644fc8b679f18ba
- lib/topics.ts: 54ed63eedcf07090896228e3f7cef3a209b31a16a59a478c70fa7c2e0e8cef37
- tests/ai.test.mjs: 3d2dd84e6147c2f4acaa47f43adcfab94573a623053be7b1af0b9581b723ba94
- tests/quiz-review.test.mjs: 0a108bee789908d16706d74c89aca701b6531a40d128b8e3bd1a302656d8f3fc
- tests/research-quality.test.mjs: 6fac87d70a8908243a4ac8d56b693040cab0eddf96519f15bb8aca3e17e2c593
- tests/topics.test.mjs: 6edd2fc809853c20d1a5c6bb392190c293b994fbfca6e3c71c5f3eb6f94bcf78

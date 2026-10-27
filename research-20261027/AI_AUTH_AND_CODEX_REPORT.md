# AI-AUTH-01 / Codex 예약 이전 조사 — 2026-10-27

| 항목 | 판정 | 적용 조건 |
|---|---|---|
| Groq를 여러 사용자에게 제공 | 가능, 공유 한도 | 한도는 조직 단위. 사용자별 동시 요청/사용량 제한과 전체429대기를 서버에 구현해야 함. 키는 서버만 보관 |
| ChatGPT 로그인 | 현재 신원 확인 | 요금제 추론 사용 권한과 별개 |
| 개인 ChatGPT 요금제 추론 | 조건부 | 지원 앱, 명시적 plan 사용 동의와 기존 한도 소진 안내 필요 |
| 원격 호스팅 PACE의 plan 사용 | 현재 미승인/미검증 | 공식 대기목록/접근 신청과 지원 확인 전 사용자에게 제공하지 않음 |
| Groq와 plan 병행 | 설계 가능, 미구현 | 공급자를 명시 선택; 각각 동의·사용량·오류·연결해제. 자동 유료 fallback 없음 |
| 기존 예약 ID의 Codex 이전 | 현재 도구로 불가 | update 도구에 host/project/agent 변경 필드 없음. 기존 실행 chat_ref.type=chatgpt 실제 확인 |
| 데스크톱 Codex 예약 | 대안 | 프로젝트/worktree를 선택하고 PC와 앱 실행 유지. 별도 시험 후 기존 예약을 중지하는 교체 경로. 새 예약은 만들지 않았음 |

공식 출처(실제 읽음):
- https://console.groq.com/docs/rate-limits — organization-level limits;429와 조직별 정확한 한도 확인.
- https://learn.chatgpt.com/docs/sign-in-with-chatgpt — 로그인과 plan permission 분리, 기존 usage에 산입, 연결해제 가능.
- https://learn.chatgpt.com/cookbook/articles/sign-in-with-chatgpt — locally running open-source/personal projects와 remotely hosted/paid apps 접근 신청 구분.
- https://learn.chatgpt.com/docs/automations — 데스크톱 프로젝트 예약과 PC/app 실행 조건.

PACE 적용 제안(메인 소유 운영 경로): app/api/ai/route.ts의 인증 사용자별 admission control과 조직 공유 semaphore/429 retry-after 안내; 공급자 선택은 실제 승인 후 서버 경로에서 검증. 문서 검토는 실제 앱 승인·추론 성공을 의미하지 않는다. app/api/**, OAuth, 계정, 키, 환경설정은 수정하지 않았다. 쿠키/세션 복사·계정 공유·과금 우회 없음. 실모델 검증 없음.

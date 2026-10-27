# 검색001 검토: 관련성 실패 재현 — PACE-DELEGATE-20261027-006

기준 작업: https://github.com/minsec2314-cloud/pace-ai-work/blob/handoff/main22-ui-20261027/README.md

RESEARCH-QUALITY-001 ZIP13869bytes/SHA256 4b229cdd7db602015ffd2b766dcc12e6b3df1557355704eea68b35c71b8c7cf6 수신, 기준main22의2파일008해시와추가패치/제출해시 일치 확인. 별도 main22 후보에서 기존200개·타입 통과. 아래 추가 관련성 실패 때문에 통합/배포 보류이며 빌드는 아직 실행하지 않았습니다. 문학/UI 코드 혼입은 없었습니다.

유료 호출 없는 실제 researchMatches 함수 재현:
1. query='차세대 전지 납', Source.title='Next generation sodium-ion batteries', abstract='' → actual true, expected false. 실제 providerQuery='next generation batteries 납'은 납을 보존하지만 matcher의 2글자 이상 토큰 추출이 한 글자 원소 조건을 지웁니다. 납뿐 아니라 다른 의미 있는 한 글자/한 자리 조건을 묵살하지 않도록 회귀를 추가하세요.
2. query='화학전지', Source.title='고효율 태양전지의 광전 변환', abstract='' → actual true, expected false. 자료 측 /전지/ 부분일치가 화학 배터리와 태양전지/광전 변환을 구분하지 않습니다. 반대로 화학 배터리와 태양전지를 함께 비교하는 실제 관련 자료를 무조건 제외하는 과잉차단도 피하고 근거 범위를 정직하게 유지하세요.
3. query='나트륨 이온 전지', Source.title='Sodium-ion batteries for grid storage', abstract='' → true 정상.

Source의 기타 필드는 id='10.1234/test',url='https://doi.org/10.1234/test',authors='Synthetic',year='2026',provider='Synthetic'로 동일했습니다. 실제 논문/실제모델 평가 결과가 아니라 함수의 합성 반례입니다. 같은 입력의 실패→수정 후 통과와 기존 DOI/형식/HTTP/추가조건 회귀 보존을 포함해 연구검색 독립002로 반환하세요. 메인은 보조 파일을 대신 수정하지 않습니다.

질의변환 공개 제안은 접수했으며 아직 운영 API/UI에 적용하지 않았습니다. 문학009 미완성과UI002는 분리 보존, 기존 누적본 중복 적용 금지. 문학 키 의존성은005와 동일하며 선택자료 검증은 계속하세요.

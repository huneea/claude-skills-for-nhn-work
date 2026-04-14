## AI-TF-VectorSearch
### <span style="color: rgb(32, 125, 229);">API</span>
##### <span style="color: rgb(0, 107, 117);">업무지원 가이드, 하모니 복리후생 가이드 NA(AD법인) 사번 검색 이슈 수정</span> <span style="color: red;">[완료]</span>
* v1 검색 API에서 특정 타겟(employee-guide, harmony-benefits-guide) 검색 안 되는 이슈 해결
    * 원인 : 공용계정 포함 코드(하드코드) 위치 오류 (2025-12-30 후쿠오카 법인 임시사번 추가 시점부터 발생)
    * 사번 제한 검색 옵션 추가 이후, 사번 필드가 없는 타겟에서 검색 결과 미반환
* PR 수정 반영

##### <span style="color: rgb(0, 107, 117);">V1 검색 rerank 로직 변경</span> <span style="color: red;">[완료]</span>
* 검색 결과 rerank 방식 변경
    * AS-IS : 타겟별 검색 → 각자 rerank → 결과 머지
    * TO-BE : 타겟별 검색 → 결과 머지 → rerank

##### <span style="color: rgb(0, 107, 117);">공용 임시사번 추가 법인 변경</span> <span style="color: red;">[완료]</span>
* 공용 임시사번(NE92622/JP96076) 사용 범위를 특정 법인으로 제한
    * NE92622 : Shared 법인 (NE, CL, ND, EP, CK)
    * JP96076 : 일본 아뜰리에 법인 (JP, PA, GJ, CO)

### <span style="color: rgb(32, 125, 229);">설계</span>
##### <span style="color: rgb(0, 107, 117);">Playground BE, VectorSearch DB 통합 논의</span> <span style="color: red;">[완료]</span>
* Playground BE - ERD와 VectorSearch - ERD 구조 차이 분석
    * 주요 차이 : 소스 테이블 분리 여부, 스페이스 저장 데이터 범위
* 진행 방향 2가지 안 정리
    * 1안) 독립 시스템 구축 후 필요 부분만 동기화 (웹훅/미들웨어/폴링)
    * 2안) Playground BE ERD 구조 변경 후 API 제공

## AI-Care-Chat
### <span style="color: rgb(32, 125, 229);">모델 성능 테스트</span>
##### <span style="color: rgb(0, 107, 117);">Gemma4-31B-IT 모델 성능 테스트</span> <span style="color: red;">[완료]</span>
* AI생활지원사 시나리오 기반 LLM 성능 비교 (GPT-4.1 vs Gemma4-31B-IT)
    * 응답 속도 : Gemma4-31B-IT 평균 650ms, GPT-4.1 평균 1,263ms
    * 답변 품질 : GPT-4.1 91점(대체 가능), Gemma4-31B-IT 89점(조건부 사용 가능)

##### <span style="color: rgb(0, 107, 117);">Gemma4-26B-A4B-it 모델 성능 테스트</span> <span style="color: red;">[완료]</span>
* AI생활지원사 시나리오 기반 LLM 성능 비교 (GPT-4.1 vs Gemma4-26B-A4B-it)
    * 응답 속도 : Gemma4-26B-A4B-it 평균 442ms, GPT-4.1 평균 1,145ms
    * 답변 품질 : GPT-4.1 92점(대체 가능), Gemma4-26B-A4B-it 88점(조건부 사용 가능)

## AI-Emo-Chat
### <span style="color: rgb(32, 125, 229);">커스터마이징</span>
##### <span style="color: rgb(0, 107, 117);">AI정서지원톡 커스터마이징 작업</span> <span style="color: red;">[완료]</span>
* 페르소나 및 에이전트 프롬프트 변경 (IIMS2 어드민)
* 와플랫 API 변경
    * 대화 리포트 API 신규 추가, 지표 항목 변경 (걸음수 증가 추세 지표 추가)
    * API 공통 응답 스펙 호환 처리, 지표 저장 API 신규 추가
* 대화 시나리오 변경
    * 서비스 제안 단계 삭제, 대화 종료시 리포트 API 호출 추가
    * 체크포인트 테이블 스키마 변경 (DBA 권고)

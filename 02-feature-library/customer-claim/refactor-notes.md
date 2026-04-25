# 고객 청구 파일 접수 기능 리팩터링 메모

## 현재 목표

insurance 프로젝트의 고객 청구 파일 접수 흐름을 다른 프로젝트에서도 사용할 수 있는 고객 서류 제출 기능 자산으로 정리한다.

## 리팩터링 방향

### 1. 보험 청구 도메인과 범용 접수 구조 분리

보험에서는 청구 접수로 사용하지만, 표준 기능 자산에서는 고객 파일 접수 또는 고객 서류 제출 구조로 관리한다.

범용 명칭 후보:

- customer-intake
- customer-file-request
- customer-submission
- document-intake

### 2. 고객 화면과 내부 화면 분리

고객은 모바일 중심의 단순 제출 화면을 사용한다.

내부 담당자는 PC 중심의 접수 관리 화면을 사용한다.

### 3. 파일관리 기능과 분리

접수 기능은 파일 자체를 직접 저장하지 않고, 파일관리 기능에서 생성된 fileId를 접수 내역에 연결한다.

권장 흐름:

```text
customer submit -> file storage -> file metadata -> claim/intake record -> staff review
```

### 4. 상태 관리 표준화

프로젝트마다 상태명은 달라질 수 있으므로 내부 상태와 표시명을 분리한다.

상태 후보:

- requested
- submitted
- reviewing
- need_more_info
- completed
- rejected
- cancelled

### 5. 메시지 기능 연결

추가 요청, 보완 요청, 처리 안내는 personal-message 기능과 연결 가능하게 둔다.

## 표준 모듈 후보

```text
CustomerIntakePage
CustomerFileSubmitForm
CustomerSubmissionStatus
StaffIntakeList
StaffIntakeDetail
IntakeStatusBadge
IntakeCommentBox
```

## 검증 항목

- 고객 링크 진입 가능
- 고객 파일 제출 가능
- 접수 내역 생성 가능
- 담당자 목록에서 확인 가능
- 접수 상세에서 파일 확인 가능
- 상태 변경 가능
- 추가 요청 메시지 연결 가능
- 고객이 타 고객 접수에 접근 불가
- 모바일 화면에서 파일 첨부 UX 정상

## 남은 TODO

- insurance 프로젝트 내 실제 원본 코드 위치 확인
- 고객앱 연결 코드 기능과 분리/연결 범위 정리
- personal-message 기능과의 연결 구조 정리
- storage-r2 기능과의 연결 예시 작성
- clean-version 작성 여부 결정

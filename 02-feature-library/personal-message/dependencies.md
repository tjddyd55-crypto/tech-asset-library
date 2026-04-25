# 개인 메시지 기능 의존성

## 관련 기능 자산

- customer-claim: 청구 보완 요청, 파일 제출 요청과 연결 가능
- storage-r2: 메시지 첨부파일 기능과 연결 가능
- notification: 알림센터 또는 푸시 알림과 연결 가능
- customer-link: 고객앱 연결 코드와 연결 가능

## 프론트 구성 요소

### 발신자 화면

- 수신자 선택
- 메시지 작성 폼
- 첨부파일 선택
- 발송 버튼
- 보낸 메시지 목록
- 메시지 상세
- 답변 확인

### 수신자 화면

- 받은 메시지 목록
- 메시지 상세
- 답변/코멘트 작성
- 읽음 표시
- 첨부파일 확인

## 서버 구성 요소

- 메시지 생성
- 수신자 연결
- 메시지 목록 조회
- 메시지 상세 조회
- 읽음 처리
- 답변/코멘트 등록
- 첨부파일 연결
- 권한 확인

## 데이터 구조 후보

### 메시지

```text
message_id
sender_type
sender_id
recipient_type
recipient_id
target_type
target_id
title
body
status
created_at
sent_at
read_at
```

### 메시지 코멘트

```text
comment_id
message_id
author_type
author_id
body
created_at
```

### 메시지 첨부파일

```text
message_file_id
message_id
file_id
created_at
```

## 권한 확인 항목

- 누가 메시지를 보낼 수 있는가
- 누구에게 보낼 수 있는가
- 수신자는 본인 메시지만 볼 수 있는가
- 발신자는 자신이 보낸 메시지만 볼 수 있는가
- 관리자는 어디까지 조회할 수 있는가
- 첨부파일 접근 권한이 메시지 권한과 일치하는가

## 주의사항

- 고객에게 보이는 메시지와 내부 메모를 분리한다.
- 전체 공지와 개인 메시지를 혼동하지 않는다.
- 답변이 필요한 메시지와 단순 안내 메시지를 구분할 수 있게 한다.
- 메시지에 업무 대상이 연결될 수 있도록 targetType, targetId를 둔다.

# 개인 메시지 기능 리팩터링 메모

## 현재 목표

insurance 프로젝트의 개인 메시지 기능을 고객 커뮤니케이션과 업무 연결이 가능한 범용 메시지 기능 자산으로 정리한다.

## 리팩터링 방향

### 1. 공지와 개인 메시지 분리

전체 공지, 소식지, 게시판과 개인 메시지는 목적이 다르다.

- 공지: 다수에게 일방향 전달
- 개인 메시지: 특정 대상에게 개별 전달
- 코멘트: 메시지 또는 업무에 대한 답변/대화

### 2. 발신자/수신자 모델 표준화

프로젝트마다 사용자 종류가 다르므로 senderType, recipientType으로 확장 가능하게 둔다.

예시:

- admin
- staff
- agent
- customer
- partner
- company
- team

### 3. 업무 대상 연결

메시지는 단독으로 존재할 수도 있고, 특정 업무와 연결될 수도 있다.

연결 예시:

- claim
- contract
- order
- audition
- escrow_step
- customer_file

### 4. 고객 노출 정보와 내부 정보 분리

고객앱에 보이는 메시지와 내부 담당자 메모는 반드시 분리한다.

### 5. 알림 기능과 느슨하게 연결

메시지 발송 시 알림을 보낼 수 있지만, 메시지 기능이 특정 알림 채널에 고정되면 안 된다.

## 표준 모듈 후보

```text
MessageComposer
RecipientSelector
SentMessageList
ReceivedMessageList
MessageDetail
MessageThread
MessageCommentForm
MessageStatusBadge
```

## 상태 후보

```text
draft
sent
read
replied
archived
cancelled
```

## 검증 항목

- 특정 수신자에게 메시지 발송 가능
- 수신자는 본인 메시지만 조회 가능
- 발신자는 보낸 메시지 확인 가능
- 읽음 처리 가능
- 답변/코멘트 등록 가능
- 업무 대상과 메시지 연결 가능
- 첨부파일 권한이 메시지 권한과 일치
- 고객앱 화면에서 내부 정보 노출 없음

## 남은 TODO

- insurance 프로젝트 내 실제 원본 코드 위치 확인
- 전체 소식지 기능과 분리 기준 정리
- notification 기능과 연결 방식 정리
- customer-claim 기능과 연결 예시 작성
- clean-version 작성 여부 결정

# R2/S3 파일관리 기능 의존성

## 프론트 구성 요소

- 파일 선택 UI
- 파일 목록 UI
- 폴더 트리 UI
- 진행 상태 표시
- 확인 모달
- 빈 상태 화면
- 오류 안내 화면

## 서버 구성 요소

- 파일 등록 처리
- 파일 목록 조회
- 파일 접근 제어
- 파일 메타데이터 관리
- 저장공간 사용량 계산
- 관리자 설정 관리
- 정리 작업

## 저장소 후보

- Cloudflare R2
- AWS S3
- 로컬 스토리지
- 외부 드라이브 연동

## 데이터 구조 후보

### 파일 메타데이터

```text
file_id
owner_type
owner_id
target_type
target_id
folder_id
original_name
mime_type
size_bytes
storage_provider
storage_key
created_by
created_at
status
```

### 저장공간 정책

```text
scope_type
scope_id
limit_bytes
used_bytes
updated_at
```

## 권한 확인 항목

- 파일을 등록할 수 있는 사용자
- 파일을 볼 수 있는 사용자
- 파일을 관리할 수 있는 사용자
- 개인, 고객, 팀, 회사 범위 구분
- 관리자 설정 가능 범위

## 주의사항

- 실제 파일과 메타데이터의 정합성을 유지한다.
- 파일 크기와 종류를 검증한다.
- 고객 파일과 내부 파일의 접근 범위를 분리한다.
- 저장공간 정책은 개인, 팀, 회사 단위로 확장 가능하게 둔다.

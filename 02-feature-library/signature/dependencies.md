# 손사인 기능 의존성

## 프론트 의존성

손사인 기능은 기본적으로 HTML Canvas 또는 SVG 기반 입력 패드로 구현할 수 있다.

필수 후보:

- React
- Canvas API
- Pointer Events
- Touch Events

선택 후보:

- 서명 패드 라이브러리
- 이미지 압축/변환 유틸
- 파일 업로드 클라이언트
- PDF 삽입 모듈

## 백엔드 의존성

손사인 기능 자체는 백엔드에 강하게 의존하지 않는다.

저장 방식에 따라 아래 구조 중 하나를 선택한다.

- base64 문자열 저장
- Blob/File 업로드
- R2/S3 업로드
- DB 메타데이터 + 스토리지 파일 저장
- PDF 생성 시 임시 이미지로 사용

## 스토리지 의존성

프로젝트별로 선택한다.

- R2
- S3
- 로컬 파일 시스템
- DB 직접 저장
- Google Drive 연동

## PDF 연동 의존성

PDF에 서명을 삽입하는 경우 아래 기능과 연결될 수 있다.

- PDF 좌표 기반 자동화
- pdf-lib
- jsPDF
- 서버 PDF 생성기
- 신청서 템플릿 관리

## 권한 의존성

서명 저장 시 다음 권한을 확인해야 한다.

- 누가 서명할 수 있는가
- 누구의 문서에 서명하는가
- 서명 후 수정 가능한가
- 서명 삭제/재작성 권한은 누구에게 있는가
- 서명 이력/Audit이 필요한가

## 데이터 모델 후보

```text
signature_id
owner_type
owner_id
target_type
target_id
image_url or image_base64
storage_key
created_by
created_at
updated_at
status
```

## 주의사항

- 기능 내부에서 특정 스토리지나 DB 테이블을 강제하지 않는다.
- 서명 이미지는 가능하면 투명 배경 PNG로 저장한다.
- 모바일 터치 스크롤과 서명 입력이 충돌하지 않도록 처리한다.
- 빈 캔버스 저장을 막는다.

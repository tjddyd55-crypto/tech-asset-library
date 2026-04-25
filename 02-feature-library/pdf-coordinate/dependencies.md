# PDF 좌표 자동화 기능 의존성

## 프론트 의존성

PDF 좌표 자동화 기능은 PDF 미리보기, 좌표 선택, 필드 매핑 UI가 필요하다.

필수 후보:

- React
- PDF 렌더링 라이브러리
- 좌표 선택 UI
- 폼 상태 관리
- 파일 다운로드 처리

선택 후보:

- PDF.js 계열 렌더링
- Canvas 기반 오버레이
- 드래그 앤 드롭 좌표 편집
- 좌표 목록 테이블
- 확대/축소 기능

## 백엔드 의존성

최종 PDF를 서버에서 생성하는 경우 백엔드에서 다음 기능이 필요하다.

- PDF 템플릿 파일 조회
- 좌표 매핑 데이터 조회
- 업무 데이터 조회
- PDF에 텍스트/이미지 삽입
- 생성된 PDF 저장 또는 다운로드 응답

## 스토리지 의존성

프로젝트별로 선택한다.

- R2
- S3
- 로컬 파일 시스템
- DB 메타데이터 + 오브젝트 스토리지
- 외부 드라이브 연동

## 데이터 모델 후보

### PDF 템플릿

```text
pdf_template_id
template_name
template_type
file_url
storage_key
version
status
created_by
created_at
updated_at
```

### PDF 좌표 필드

```text
field_id
pdf_template_id
page_index
field_key
field_label
field_type
x
y
width
height
font_size
align
required
sort_order
created_at
updated_at
```

### PDF 생성 이력

```text
generated_pdf_id
pdf_template_id
target_type
target_id
file_url
storage_key
generated_by
generated_at
```

## 권한 의존성

- 누가 템플릿을 등록할 수 있는가
- 누가 좌표를 수정할 수 있는가
- 누가 PDF를 생성할 수 있는가
- 누가 생성된 PDF를 볼 수 있는가
- 고객이 볼 수 있는 PDF와 내부 관리자가 볼 수 있는 PDF를 분리해야 하는가

## 손사인 기능과의 연결

서명 필드는 `signature` 타입으로 관리하고, 손사인 기능에서 생성된 이미지 데이터를 PDF 삽입 데이터로 전달한다.

## 주의사항

- 좌표값은 PDF 렌더링 크기와 실제 PDF 좌표계의 차이를 고려해야 한다.
- 확대/축소 상태에서 찍은 좌표가 실제 PDF 생성 좌표와 어긋나지 않게 보정해야 한다.
- 한글 폰트 삽입이 필요한 경우 폰트 임베딩 전략을 별도로 둔다.
- PDF 템플릿 버전 변경 시 기존 좌표가 깨질 수 있으므로 버전 관리를 고려한다.

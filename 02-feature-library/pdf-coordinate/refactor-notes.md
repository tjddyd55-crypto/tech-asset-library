# PDF 좌표 자동화 기능 리팩터링 메모

## 현재 목표

insurance 프로젝트에서 개발 또는 계획된 PDF 좌표 자동화 기능을 여러 프로젝트에서 재사용 가능한 문서 자동화 자산으로 정리한다.

## 리팩터링 방향

### 1. 템플릿과 좌표 분리

PDF 파일 자체와 좌표 필드 정보는 분리해서 관리한다.

- PDF 템플릿: 파일, 이름, 버전, 상태
- 좌표 필드: 페이지, 위치, 크기, 필드키, 타입

### 2. 도메인 데이터와 분리

PDF 생성 모듈은 고객, 계약, 청구, 주문 같은 원본 도메인 객체를 직접 알지 않도록 한다.

프로젝트별 mapper가 도메인 데이터를 PDF fieldKey 데이터로 변환한다.

권장 구조:

```text
domain data -> pdf data mapper -> fieldKey data -> pdf generator
```

### 3. 좌표계 보정

PDF 미리보기 화면 크기와 실제 PDF 좌표계가 다를 수 있으므로 다음 값을 함께 고려한다.

- 원본 PDF 페이지 크기
- 화면 렌더링 크기
- 확대/축소 배율
- 좌표 변환 비율
- 페이지 인덱스

### 4. 필드 타입 표준화

기본 필드 타입을 표준화한다.

- text
- date
- number
- checkbox
- radio
- image
- signature
- multilineText

### 5. 서명 기능 연결

signature 필드는 손사인 기능에서 생성한 이미지 데이터를 사용한다.

서명 이미지는 비율과 투명 배경을 유지해야 한다.

## 표준 모듈 후보

```text
PdfTemplateManager
PdfCoordinateEditor
PdfFieldList
PdfPreviewCanvas
PdfDataMapper
PdfGenerator
PdfDownloadButton
```

## 검증 항목

- PDF 템플릿 등록 가능
- 페이지별 좌표 저장 가능
- 좌표 수정/삭제 가능
- fieldKey 매핑 가능
- 테스트 데이터로 미리보기 가능
- 한글 텍스트 삽입 가능
- 서명 이미지 삽입 가능
- 생성된 PDF 다운로드 가능
- 모바일에서는 좌표 편집 대신 조회/서명 중심 UX로 분리 가능

## 남은 TODO

- insurance 프로젝트 내 실제 원본 코드 위치 확인
- 좌표 저장 DB 구조 확인
- PDF 생성 위치가 프론트인지 서버인지 확인
- 한글 폰트 처리 방식 확인
- clean-version 작성 여부 결정

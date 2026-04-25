# 손사인 기능 리팩터링 메모

## 현재 목표

insurance 프로젝트에서 개발된 손사인 기능을 다른 프로젝트에도 재사용할 수 있는 표준 기능 자산으로 정리한다.

## 리팩터링 방향

### 1. UI와 저장 로직 분리

서명 입력 컴포넌트는 서명 데이터만 생성한다.

저장은 외부에서 처리한다.

- DB 저장
- R2/S3 업로드
- PDF 삽입
- 신청서 연결
- 고객/계약/청구 데이터 연결

### 2. 입력 이벤트 통합

PC와 모바일을 모두 지원해야 한다.

- Pointer Events 우선 검토
- Mouse Events fallback
- Touch Events fallback
- 모바일 스크롤 충돌 방지

### 3. 결과 데이터 표준화

서명 결과는 최소 아래 형태 중 하나로 반환 가능해야 한다.

- base64 PNG
- Blob
- File
- dataUrl

권장 반환 형태:

```ts
type SignatureResult = {
  dataUrl: string
  blob?: Blob
  width: number
  height: number
  isEmpty: boolean
}
```

### 4. 프로젝트 고정값 제거

아래 값들은 컴포넌트 내부에 넣지 않는다.

- customerId
- claimId
- documentId
- applicationId
- storageKey
- API endpoint
- DB table name
- tenant/company/team id

### 5. PDF 자동화 연결 고려

PDF 좌표 자동화 기능과 연결될 수 있도록 서명 이미지의 크기, 비율, 투명 배경을 유지한다.

## 표준 컴포넌트 후보

```text
SignaturePad
SignaturePreview
SignatureModal
useSignatureCanvas
signatureToBlob
signatureToFile
```

## 검증 항목

- PC 마우스로 서명 가능
- 모바일 터치로 서명 가능
- 다시 쓰기 가능
- 빈 서명 저장 방지
- 저장 콜백 정상 호출
- 투명 배경 이미지 생성 가능
- 작은 모바일 화면에서 사용 가능
- PDF 삽입 시 비율 깨짐 없음

## 남은 TODO

- insurance 프로젝트 내 실제 원본 코드 위치 확인
- clean-version 작성 여부 결정
- PDF 좌표 자동화 기능과 연결 방식 문서화
- 저장소 어댑터 예시 작성

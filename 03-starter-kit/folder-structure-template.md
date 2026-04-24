# 폴더 구조 템플릿

```text
project-root/
  docs/
  apps/
    web/
    mobile-web/
    admin/
    native-app/          # 필요 시 별도 레포로 분리 가능
  services/
    api/
    batch/
    worker/
  packages/
    domain/
    application/
    infrastructure/
    ui/
    shared/
  tests/
    e2e/
    integration/
```

## 설계 의도

- 실행 단위(`apps`, `services`)와 재사용 단위(`packages`)를 분리한다.
- 도메인 규칙은 `packages/domain` 중심으로 유지한다.
- 인프라 세부 구현은 `packages/infrastructure`에 한정한다.

## 적용 규칙

- 기능 추가 시 먼저 어느 레이어 변경인지 명시한다.
- 공통 패키지 변경 시 영향 범위를 문서화한다.
- 플랫폼 전용 코드는 공통 패키지로 올리지 않는다.

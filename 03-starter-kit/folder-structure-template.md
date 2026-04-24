# 폴더 구조 템플릿

## 업무형 SaaS 기본 구조

```text
project-name/
  apps/
    web-pc/
    web-mobile/
    mobile-app/
    desktop-app/

  packages/
    shared-ui/
    shared-api/
    shared-types/
    design-system/
    feature-signature/
    feature-pdf-coordinate/
    feature-storage/
    feature-message/

  server/
    apis/
    db/
    services/
    auth/
    permissions/
    storage/
    jobs/

  docs/
    architecture.md
    feature-list.md
    design-system.md
    development-plan.md
```

## 단일 Next.js 스타터 구조

```text
project-name/
  src/
    app/
    components/
    features/
    server/
    lib/
    styles/

  prisma/
  docs/
  scripts/
```

## Spring Boot + Next.js 구조

```text
project-name/
  backend/
    src/
    build.gradle or pom.xml

  frontend/
    web/

  docs/
```

## 기술자산 적용 방식

- 새 프로젝트는 처음부터 필요한 플랫폼 구조를 선택한다.
- 기능은 feature-library에서 선택한다.
- 공통 디자인은 design-system 기준을 따른다.
- 기능별 코드는 원본 프로젝트에서 직접 복사하지 않고 정리된 적용 지시문 기준으로 붙인다.

# mementomoriCarpediem.github.io

공명(Gongmyung) — 회사·서비스 통합 소개 페이지 (GitHub Pages 유저 사이트)

Jekyll 정적 사이트로 구성되어 있으며, `main` 브랜치에 배포 시 `https://mementomoricarpediem.github.io`에 게시됩니다.

## 로컬 실행

```bash
bundle install
bundle exec jekyll serve
```

기본적으로 `http://127.0.0.1:4000`에서 확인할 수 있습니다.

빌드만 하려면:

```bash
bundle exec jekyll build
```

결과물은 `_site/`에 생성됩니다 (git에는 커밋되지 않음).

## 구조

- `_config.yml` — 사이트 전역 설정 (title, url, plugins, collections 등)
- `_layouts/default.html` — 공통 레이아웃 (헤더/푸터/SEO)
- `assets/css/style.css` — 사이트 스타일
- `index.md` — 홈(회사 소개) 페이지
- `services.md` — 서비스 목록 페이지 (`/services/`)
- `_services/` — 서비스별 상세 페이지를 담는 collection
- `services/<app-id>/` — 서비스(앱)별 스토어 제출용 법적 고지 페이지 (개인정보처리방침/이용약관/고객지원, `/services/<app-id>/{privacy-policy,terms,support}/`)
- `_templates/` — 신규 서비스용 법적 고지 페이지 템플릿 (빌드 제외 대상)
- `404.html` — 404 페이지
- `robots.txt` — 크롤러 정책 + sitemap 경로

## 서비스 추가 방법

새 서비스를 소개 페이지에 추가하려면 `_services/` 디렉토리에 마크다운 파일 1개만 추가하면 됩니다.

1. `_services/<service-id>.md` 파일 생성 (예: `_services/my-service.md`)
2. 아래 front matter 스키마를 따라 작성:

   ```yaml
   ---
   layout: default
   title: "서비스명"
   description: "검색엔진에 노출될 설명 문구"
   summary: "카드에 노출될 한 줄 요약"
   external_url: "https://example.com"
   order: 4
   ---

   서비스 소개 본문 (1~2문단)

   <p>
     <a class="btn" href="{{ page.external_url }}" target="_blank" rel="noopener">공식 페이지 방문 →</a>
   </p>
   ```

3. `order` 값으로 홈/서비스 목록 페이지에서의 정렬 순서를 지정합니다.
4. 빌드하면 `/services/<service-id>/` 경로로 자동 생성되며, 홈(`index.md`)과 서비스 목록(`services.md`) 카드 그리드에도 자동으로 나타납니다. 별도의 링크 추가 작업이 필요 없습니다.

### 법적 고지 페이지(개인정보처리방침/이용약관/고객지원) 추가 방법

앱스토어/플레이스토어 제출 시 요구되는 privacy-policy · terms · support 문서를 서비스별로 `/services/<app-id>/` 하위에 둡니다.

1. `_templates/` 디렉토리의 3개 템플릿을 새 서비스 디렉토리로 복사합니다.

   ```bash
   mkdir -p services/<app-id>
   cp _templates/privacy-policy-template.md services/<app-id>/privacy-policy.md
   cp _templates/terms-template.md services/<app-id>/terms.md
   cp _templates/support-template.md services/<app-id>/support.md
   ```

2. 각 파일에서 `{{APP_NAME}}` / `{{CONTACT_EMAIL}}` / `{{EFFECTIVE_DATE}}` 플레이스홀더와 `permalink`의 `REPLACE_ID`를 실제 `<app-id>`로 치환합니다.
3. `<!-- TODO: 앱별 확인 필요 -->` 주석이 달린 조항(수집 항목, 제3자 제공, 위탁 업체 등)을 실제 서비스 데이터 처리 현황에 맞게 채웁니다.
4. 해당 서비스의 `_services/<app-id>.md` front matter에 `legal: true`를 추가하면 서비스 상세 페이지 하단에 3개 문서 링크가 자동으로 노출됩니다 (레이아웃의 `service-legal-links.html` 인클루드가 `page.slug` 기반으로 URL을 생성하므로 하드코딩 불필요).
5. 빌드 후 `/services/<app-id>/{privacy-policy,terms,support}/` 3개 URL이 정상 노출되는지 확인합니다.

## 배포

GitHub Pages 유저 사이트로 배포됩니다. `.github/workflows/pages.yml`의 Actions 기반 배포(`main` 브랜치 push 시 자동 빌드, `bundle exec jekyll build` → Pages 아티팩트 업로드/배포)를 사용하여 레포의 Gemfile(Jekyll 4.3)을 운영 빌드에서도 동일하게 사용합니다(로컬/운영 parity). Google Analytics, Search Console 소유권 확인 등은 이 초기 구축 범위에 포함되지 않았으며 추후 별도로 추가될 예정입니다.

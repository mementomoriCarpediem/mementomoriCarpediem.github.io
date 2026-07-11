source "https://rubygems.org"

# GitHub Pages 빌드 환경 호환 버전 고정 (jekyll ~> 4.3 — GitHub Pages 지원 버전)
# 로컬/운영 parity는 .github/workflows/pages.yml (Actions 기반 배포)로 확보 —
# 운영 빌드가 본 Gemfile(Jekyll 4.3)을 그대로 사용.
gem "jekyll", "~> 4.3"
gem "logger"
gem "csv"
gem "base64"

group :jekyll_plugins do
  gem "jekyll-seo-tag"
  gem "jekyll-sitemap"
end

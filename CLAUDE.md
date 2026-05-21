# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

Jekyll 기반 개인 기술 블로그 (dev.drawyourmind.com). Texture 테마를 커스터마이징하여 사용.

## 빌드 및 개발

```bash
bundle install              # 의존성 설치
bundle exec jekyll serve    # 로컬 개발 서버 (http://localhost:4000)
bundle exec jekyll build    # 프로덕션 빌드 (_site/ 출력)
```

## 아키텍처

- **테마**: Texture (thelehhman/texture) 기반, `_layouts/`, `_includes/`, `_sass/`에서 커스터마이징
- **레이아웃 계층**: `home.html` / `post.html` → `page.html` (공통 wrapper)
- **스타일**: `_sass/theme.scss`가 메인 스타일시트. 반응형 breakpoint — 모바일 768px, 소형 480px, 대형 1600px
- **플러그인**: jekyll-seo-tag, jekyll-paginate (10개/페이지), jekyll-feed
- **외부 서비스**: Google Analytics (G-WW18CJXG1T), Google Adsense, Disqus 댓글

## 포스트 작성 규칙

- 파일명: `_posts/YYYY-MM-DD-slug.md`
- Frontmatter 필수 항목: `layout: post`, `title`, `description`, `date`, `categories`
- 퍼머링크: `/posts/:title/`
- 포스트 이미지: `assets/images/posts/` 하위에 포스트별 디렉토리로 관리

## 커밋 메시지

- 한국어로 간결하게 작성
- Co-Authored-By 메시지 포함하지 않음

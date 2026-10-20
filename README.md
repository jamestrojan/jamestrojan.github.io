# Siwoo Han의 코딩 노트

블로그 주소: https://blog.ultramax.pro/

GitHub Pages는 `main` 브랜치를 게시한다. GitHub에 내장된 Jekyll과 Minima 테마를 사용하며, 이 저장소에는 현재 블로그 소스만 보관한다.

## 글 작성

`_posts/`에 `YYYY-MM-DD-slug.md` 형식으로 파일을 만든다. 기존 글은 `2026-10-20-c-hello-world.md`이다.

머리말은 YAML로 작성한다. 날짜에는 시간대 오프셋을 명시한다.

```yaml
---
title: 새 학습 노트
date: 2026-10-20 11:55:18 +0800
categories:
  - C 언어 학습
tags:
  - C
---
```

본문은 Markdown으로 쓴다. `<!-- more -->` 앞의 내용이 첫 화면의 요약으로 표시된다. 파일 이름의 slug가 `/posts/slug/` 주소를 결정하므로 게시 후에는 유지한다.

기존 글을 수정할 때는 원래 `date`를 유지하고 `last_modified_at`에 실제 수정 시간을 적는다. 이 값은 Jekyll의 검색 및 공유용 메타데이터에 사용된다.

GitHub 웹 화면에서 이 브랜치를 직접 편집할 수 있다. 이 방법에는 로컬 Ruby나 Node.js 설치가 필요하지 않다.

## 한국어와 코드 기호

- 사이트 언어는 `ko-KR`이고 날짜는 연월일 형식으로 표시한다.
- 제목, 소개, 작성자 이름과 글 내용은 사이트 설정 및 Markdown에서 관리한다.
- `_layouts/home.html`은 한국어 글 목록과 RSS 구독 문구를 제공한다.
- `_layouts/default.html`은 한국어 본문 영역 이름과 단어 단위 줄바꿈을 제공한다. 긴 단어는 필요할 때 줄바꿈할 수 있다.
- 나머지 테마 템플릿과 스타일은 Minima를 그대로 사용한다.
- 글 파일은 UTF-8로 저장한다. C의 키워드와 구문용 괄호, 따옴표, 세미콜론에는 ASCII를 사용한다.
- 글 안의 전각 기호와 스마트 따옴표는 의도적으로 잘못된 코드를 보여 주는 예시다. 마지막의 완전한 C 프로그램에는 ASCII 문자만 사용한다.

## 게시

저장소의 Pages 설정을 다음과 같이 유지한다.

- 게시 방식: `Deploy from a branch`
- 브랜치: `main`
- 폴더: `/ (root)`
- 사용자 지정 도메인: `blog.ultramax.pro`
- `Enforce HTTPS`: 활성화

이 브랜치에 변경 사항을 푸시하면 GitHub가 시스템 관리형 `pages build and deployment`를 실행한다. 별도의 사용자 작성 Actions 워크플로는 필요하지 않다. 작업 성공 여부와 실제 웹 페이지를 함께 확인한다.

로컬에서 푸시하기 전에는 GitHub가 도메인 설정을 저장하면서 만든 커밋을 먼저 동기화한다.

```powershell
git pull --ff-only
git add .
git commit -m "docs: update learning note"
git push
```

## 도메인 유지

- `_config.yml`의 `url`은 `https://blog.ultramax.pro`이고 `baseurl`은 빈 값이다.
- 이 브랜치 루트의 `CNAME` 파일은 `blog.ultramax.pro`를 포함해야 한다.
- Cloudflare의 `blog` CNAME은 이 저장소의 GitHub Pages 기본 호스트를 가리킨다. 프록시는 `DNS only`, TTL은 `Auto`로 유지한다.
- GitHub Pages 도메인 소유권 확인용 TXT 레코드를 유지한다.
- DNS 전용 모드에서 HTTPS 인증서는 GitHub가 제공한다. Cloudflare의 에지 인증서는 이 연결에 사용되지 않는다.
- 사용자 지정 도메인을 GitHub 기본 주소로 보내는 리디렉션 규칙은 만들지 않는다. 이전 기본 주소가 사용자 지정 도메인으로 이동하는 것이 의도한 동작이다.

`README.md`는 사이트 생성 대상에서 제외되어 별도의 웹 페이지나 탐색 항목으로 표시되지 않는다.

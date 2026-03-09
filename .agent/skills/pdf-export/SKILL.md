---
name: pdf-export
description: 최적화된 Markdown 이력서를 프로페셔널한 HTML(→PDF) 파일로 변환하는 스킬
---

# 프로페셔널 이력서 변환 스킬 (Professional Export)

## 목적

최적화된 이력서를 **프로페셔널한 디자인의 HTML 파일**로 직접 생성합니다.
생성 과정에 Python, npm 등 **어떤 패키지도 필요하지 않습니다.**
에이전트가 직접 HTML+CSS를 작성하여 파일로 저장합니다.

## 변환 방법

### 에이전트가 직접 HTML 생성

1. 최적화된 이력서(`.md`)의 내용을 읽습니다.
2. 아래 **HTML 템플릿 구조**에 맞춰 인라인 CSS가 포함된 HTML 파일을 `write_to_file` 도구로 직접 생성합니다.
3. `output/[회사명]_[직무명]_이력서.html` 경로에 저장합니다.

### PDF로 변환 (사용자가 수동)

생성된 HTML 파일을 브라우저에서 열고 `Cmd+P` (또는 `Ctrl+P`)로 인쇄 → **PDF로 저장**합니다.

---

## HTML 템플릿 구조

아래 구조를 따라 HTML 파일을 생성합니다. **모든 CSS는 인라인(`<style>` 태그)**으로 포함하여 외부 의존성이 없어야 합니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>[이름] - [직무명] 이력서</title>
    <link rel="preconnect" href="https://cdn.jsdelivr.net">
    <link href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css" rel="stylesheet">
    <style>
        /* 반드시 templates/resume.css의 스타일을 여기에 인라인으로 포함 */
        /* @page, body, h1~h4, table, ul, hr 등 모든 스타일 포함 */
    </style>
</head>
<body>
    <!-- 이력서 내용을 HTML 태그로 변환하여 작성 -->
    <h1>이름</h1>
    <h2>지원 포지션: 직무명 — 회사명</h2>
    <hr>
    <h3>핵심 역량 요약</h3>
    <p>...</p>
    <!-- 이하 동일한 패턴 -->
</body>
</html>
```

## 디자인 원칙

아래 `templates/resume.css` 파일의 스타일을 참조하여 적용합니다:

1. **컬러 팔레트**: 네이비(`#1a1a2e`), 다크블루(`#0f3460`), 레드 악센트(`#e94560`)
2. **폰트**: Pretendard (한글 최적화, CDN 로드)
3. **레이아웃**: A4 기준, 상하 15mm / 좌우 20mm 여백
4. **테이블**: 헤더 네이비 배경 + 짝수행 연밝은 회색
5. **섹션 구분**: `<h3>` 하단에 얇은 보더라인
6. **핵심 역량**: 왼쪽 레드 보더 + 연한 배경 강조

## 마크다운 → HTML 변환 규칙

| Markdown | HTML |
|----------|------|
| `# 제목` | `<h1>` |
| `## 지원 포지션` | `<h2>` |
| `### 섹션` | `<h3>` |
| `#### 하위 섹션` | `<h4>` |
| `- 항목` | `<ul><li>` |
| `**굵게**` | `<strong>` |
| `*이탤릭*` | `<em>` |
| `---` | `<hr>` |
| 테이블 | `<table>` |

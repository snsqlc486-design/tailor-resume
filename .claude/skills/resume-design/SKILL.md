---
name: resume-design
description: 최적화된 이력서를 사용자 맞춤 디자인의 프로페셔널한 HTML로 변환하는 스킬
---

# 이력서 디자인 스킬 (Resume Design)

## 목적

최적화된 이력서를 **프로페셔널한 디자인의 HTML 파일**로 직접 생성합니다.
생성 과정에 Python, npm 등 **어떤 패키지도 필요하지 않습니다.**
에이전트가 직접 HTML+CSS를 작성하여 파일로 저장합니다.

## 변환 방법

### 1. 디자인 선호도 확인 (HTML 생성 전 필수)

HTML 이력서를 생성하기 **전에** 사용자에게 디자인 선호도를 물어봅니다.
아래 질문을 한 번에 제시하고, 사용자의 답변을 반영하여 CSS를 조정합니다.

```
이력서를 프로페셔널한 HTML로 만들기 전에 디자인 선호도를 여쭤볼게요!

1. 🎨 **컬러 스타일** — 어떤 느낌을 원하시나요?
   a) 네이비 + 레드 악센트 (세련된 느낌) ⭐ 추천
   b) 블랙 + 골드 (고급스러운 느낌)
   c) 딥그린 + 화이트 (자연스럽고 깔끔한 느낌)
   d) 모던 그레이 (미니멀한 느낌)
   e) 직접 지정 (원하는 색상 알려주세요)

2. 📐 **레이아웃** — 선호하는 스타일은?
   a) 1단 레이아웃 (깔끔한 세로형) ⭐ 추천
   b) 2단 레이아웃 (왼쪽 사이드바 + 오른쪽 본문)

3. ✏️ **폰트 스타일** — 어떤 느낌의 글씨체?
   a) Pretendard (깔끔한 산세리프) ⭐ 추천
   b) Noto Serif KR (격식 있는 세리프)
   c) IBM Plex Sans KR (테크 느낌)

4. 📄 **분량** — 몇 페이지로 맞출까요?
   a) 1페이지 (간결하게)
   b) 2페이지 (상세하게)
   c) 자동 (내용에 맞게) ⭐ 추천

5. 💡 **기타 요청** — 추가로 원하는 디자인이 있으면 자유롭게!
   (예: "사진 넣을 공간", "GitHub 링크 포함", "아이콘 사용" 등)

숫자만 답해도 됩니다 (예: "1a, 2a, 3a, 4c") / "추천대로" 하면 ⭐ 옵션으로 진행!
```

사용자가 빠르게 답하고 싶으면 숫자만 답해도 됩니다 (예: "1a, 2a, 3a, 4c").
답변이 없거나 "기본"이라고 하면 기본 스타일(`templates/resume.css`)로 진행합니다.

### 2. 디자인 프리셋

사용자 답변에 따라 아래 프리셋을 적용합니다:

#### 컬러 프리셋

| 프리셋 | Primary | Accent | Highlight | 배경 |
|--------|---------|--------|-----------|------|
| **(a) 네이비 + 레드** | `#1a1a2e` | `#0f3460` | `#e94560` | `#f8f9fb` |
| **(b) 블랙 + 골드** | `#1a1a1a` | `#2d2d2d` | `#c9a227` | `#fafafa` |
| **(c) 딥그린 + 화이트** | `#1b4332` | `#2d6a4f` | `#40916c` | `#f7faf8` |
| **(d) 모던 그레이** | `#333333` | `#555555` | `#0077b6` | `#f5f5f5` |

#### 폰트 프리셋

| 프리셋 | CDN 링크 | font-family |
|--------|----------|-------------|
| **(a) Pretendard** | `https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css` | `'Pretendard'` |
| **(b) Noto Serif KR** | `https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@400;500;700&display=swap` | `'Noto Serif KR'` |
| **(c) IBM Plex Sans KR** | `https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+KR:wght@300;400;500;600;700&display=swap` | `'IBM Plex Sans KR'` |

### 3. HTML 생성

1. 최적화된 이력서(`.md`)의 내용을 읽습니다.
2. 사용자가 선택한 **컬러 프리셋 + 폰트 프리셋**의 CSS 변수와 CDN을 적용합니다.
3. `write_to_file` 도구로 HTML 파일을 직접 생성합니다.
4. `output/[회사명]_[직무명]_이력서.html` 경로에 저장합니다.

### PDF로 변환 (사용자가 수동)

생성된 HTML 파일을 브라우저에서 열고 `Cmd+P` (또는 `Ctrl+P`)로 인쇄 → **PDF로 저장**합니다.

---

## HTML 템플릿 구조

아래 구조를 따라 HTML 파일을 생성합니다. **모든 CSS는 인라인(`<style>` 태그)**으로 포함하여 외부 의존성이 없어야 합니다.
폰트 CDN은 사용자가 선택한 프리셋에 맞는 것을 사용합니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>[이름] - [직무명] 이력서</title>
    <!-- 사용자 선택에 맞는 폰트 CDN -->
    <link href="[선택된 폰트 CDN URL]" rel="stylesheet">
    <style>
        :root {
            --primary: [선택된 Primary];
            --accent: [선택된 Accent];
            --highlight: [선택된 Highlight];
            --bg-light: [선택된 배경];
        }
        /* 공통 레이아웃 스타일 */
        @page { size: A4; margin: 15mm 20mm; }
        body { font-family: [선택된 font-family], sans-serif; }
        /* ... 나머지 스타일 ... */
    </style>
</head>
<body>
    <!-- 이력서 내용 -->
</body>
</html>
```

## 디자인 공통 원칙

프리셋과 무관하게 아래 원칙은 항상 적용합니다:

1. **페이지**: A4 기준, 상하 15mm / 좌우 20mm 여백 (1페이지 선택 시 12mm/16mm로 축소)
2. **테이블**: 헤더 Primary 색상 배경 + 짝수행 연한 배경
3. **섹션 구분**: `<h2>` 하단에 border-bottom
4. **핵심 역량**: 왼쪽 Highlight 보더 + 연한 배경 강조
5. **인쇄 최적화**: `-webkit-print-color-adjust: exact` 적용

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

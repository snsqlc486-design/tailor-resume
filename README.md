# 📄 Resume Tailor Agent

직업 공고에 맞춰 이력서를 자동으로 최적화해주는 AI 에이전트입니다.  
코드 없이 Claude Code가 직접 이력서를 분석하고 맞춤 이력서를 생성합니다.

---

## 🚀 시작하기 (초보자 가이드)

### 필요한 것

| 항목 | 설명 |
|------|------|
| **AI 코딩 도구** | [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (터미널 CLI) |
| **이력서** | 본인의 이력서 텍스트 파일 (`이력서.txt`) |
| **직업 공고** | 지원하고 싶은 직업 공고 URL 또는 텍스트 |

> 💡 **코딩 지식 불필요!** 이 에이전트는 코드가 아닙니다. Claude에게 명령하면 알아서 해줍니다.

### 1단계: 프로젝트 다운로드

```bash
git clone https://github.com/jaewpark87/tailor-resume.git
cd tailor-resume
```

> GitHub에 올리지 않았다면 폴더를 직접 복사해도 됩니다.

### 2단계: 내 이력서 준비

프로젝트 폴더에 이력서 파일을 만들고 본인의 이력서 내용을 붙여넣습니다.

- 기본 파일명: `이력서.txt`
- 다른 이름이나 형식도 OK: `resume.md`, `내이력서.txt` 등 (`.txt`, `.md` 지원)

```
resume-tailor/
└── 이력서.txt    ← 여기에 내 이력서 내용 작성
```

**형식은 자유!** 아래처럼 작성하면 됩니다:

```
홍길동
데이터 분석가 010-1234-5678 hong@email.com

경력 사항
OO회사 데이터팀/사원
2020.01~ 2024.12 (5년)
- SQL로 일일 매출 리포트 자동화
- Python 기반 고객 이탈 예측 모델 구축
...
```

### 3단계: Claude Code에서 프로젝트 열기

터미널(맥: Terminal 앱)을 열고 아래 명령어를 순서대로 입력합니다:

```bash
# 프로젝트 폴더로 이동
cd tailor-resume

# Claude Code 실행
claude
```

> **Claude Code가 없다면?** [Claude Code 설치 가이드](https://docs.anthropic.com/en/docs/claude-code)를 참고하세요.

Claude Code가 실행되면 채팅 인터페이스가 나타납니다. 여기에 명령을 입력하면 됩니다!

### 4단계: 이력서 최적화 요청!

채팅창에 아래처럼 입력하면 끝!

```
/tailor-resume
이 공고에 맞춰 이력서 만들어줘: https://www.saramin.co.kr/zf_user/jobs/relay/view?rec_idx=12345678
```

다른 이력서 파일을 지정하고 싶다면:

```
/tailor-resume
@resume.md 이 이력서로 이 공고에 맞춰 만들어줘: https://example.com/job
```

Claude가 자동으로:
1. ✅ 내 이력서를 읽고
2. ✅ 직업 공고를 분석하고
3. ✅ 매칭 결과를 보여주고
4. ✅ 최적화된 이력서를 만들어줍니다

결과물은 `output/` 폴더에 자동 저장됩니다!

---

## 📝 예제 프롬프트

### URL로 공고 제공

```
/tailor-resume
이 공고에 맞춰 이력서 만들어줘: https://www.saramin.co.kr/zf_user/jobs/relay/view?rec_idx=12345678
```

```
/tailor-resume
https://www.wanted.co.kr/wd/123456 여기에 지원하려고 해. 이력서 최적화해줘.
```

### 텍스트로 공고 제공

```
/tailor-resume
아래 공고에 맞춰 이력서 만들어줘.

[데이터 분석가 채용]
회사: OO컴퍼니
자격요건:
- Python, SQL 활용 가능자
- 데이터 시각화 경험 (Tableau, Power BI 등)
우대사항:
- 머신러닝 모델링 경험
```

### 특정 부분 강조

```
/tailor-resume
https://example.com/job/data-analyst
데이터 분석 프로젝트 경험을 특히 강조해줘.
```

### 수정 요청

```
이력서 잘 만들어줬는데, 경력 사항에서 광고기획 경험도 좀 더 넣어줘.
```

### 프로페셔널 HTML 출력

```
이력서 프로페셔널하게 HTML로도 만들어줘
```

### 전문가 리뷰 요청

```
이력서 전문가 리뷰 해줘
```

```
HR 입장에서 이력서 리뷰 해줘
```

```
이력서 디자인 리뷰 해줘
```

```
리뷰 피드백 반영해서 이력서 수정해줘
```

---

## ⚙️ 에이전트 동작 흐름

```
1. 이력서 읽기        →  이력서 파일에서 원본 경력/기술/학력 파악
2. 직업 공고 분석     →  필수요건, 우대사항, 핵심 키워드 추출
3. 매칭 분석          →  이력서 ↔ 공고 정직한 매칭 분석
4. 전문가 사전 리뷰   →  👔HR / 🎯취업전문가가 최적화 전략 리뷰
5. 이력서 생성        →  리뷰 반영된 최적화 이력서 생성
6. 저장 및 리뷰       →  output/에 저장, 사용자 확인
7. HTML 변환 (선택)   →  디자인 선호도 질문 → 맞춤 HTML 생성
8. 디자인 리뷰 (선택) →  🎨디자이너 리뷰 + CSS 적용
```

---

## 🎨 프로페셔널 출력 (HTML → PDF)

HTML 변환 요청 시 에이전트가 **디자인 선호도**를 먼저 물어봅니다:

- 🎨 컬러 스타일 (4가지 프리셋 + 직접 지정)
- 📐 레이아웃 (1단/2단)
- ✏️ 폰트 (Pretendard, Noto Serif, IBM Plex Sans)
- 📄 분량 (1p/2p/자동)

**PDF가 필요하면?**  
생성된 `.html` 파일을 브라우저에서 열고 → `Cmd+P` (Mac) / `Ctrl+P` (Windows) → **PDF로 저장**

---

## 📁 파일 구조

```
resume-tailor/
├── 이력서.txt                          # 🔒 내 이력서 (git에 포함되지 않음)
├── README.md                           # 이 파일
├── output/                             # 🔒 생성된 이력서 (git에 포함되지 않음)
└── .agent/
    ├── agent.md                        # 에이전트 역할 및 원칙 정의
    ├── workflows/
    │   └── tailor-resume.md            # /tailor-resume 워크플로우
    └── skills/
        ├── job-analysis/
        │   └── SKILL.md                # 직업 공고 분석 스킬
        ├── resume-design/
        │   ├── SKILL.md                # 이력서 디자인 스킬
        │   └── templates/
        │       └── resume.css          # 기본 디자인 스타일
        └── resume-review/
            └── SKILL.md                # 👔HR/🎯취업전문가/🎨디자인 리뷰 스킬
```

---

## ❓ FAQ

**Q: 코딩을 전혀 몰라도 사용할 수 있나요?**  
A: 네! Claude Code에서 채팅하듯 요청하면 됩니다.

**Q: 이력서에 없는 내용이 추가되나요?**  
A: 아닙니다. 에이전트는 원본에 **없는 기술·경험·도구를 절대 날조하지 않습니다.** 공고에서 요구하지만 이력서에 없는 항목은 "부족한 부분"으로 알려주고, 추가하지 않습니다.

**Q: HTML 디자인을 내 취향대로 만들 수 있나요?**  
A: 네! HTML 변환 시 에이전트가 컬러, 레이아웃, 폰트, 분량 등을 물어봅니다. `"추천대로"` 하면 기본 스타일로 진행됩니다.

**Q: 여러 공고에 동시에 지원할 수 있나요?**  
A: 네! 공고마다 `/tailor-resume`을 실행하면 각각 다른 최적화 이력서가 `output/` 폴더에 저장됩니다.

**Q: 이력서 내용을 수정하고 싶으면?**  
A: `이력서.txt`를 수정하면 다음 실행 시 자동 반영됩니다.

**Q: 개인정보가 유출될 수 있나요?**  
A: `이력서.txt`와 `output/` 폴더는 `.gitignore`에 등록되어 있어 git에 커밋되지 않습니다.

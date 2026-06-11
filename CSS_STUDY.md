# index.html CSS 정리

이 문서는 `index.html`에 작성된 CSS를 공부용으로 정리한 자료입니다.

## 1. 웹폰트 불러오기

```css
@font-face {
  font-family: 'GapyeongHanseokbongBigBrush';
  src: url('...woff2') format('woff2');
  font-weight: 300;
  font-display: swap;
}
```

`@font-face`는 외부 폰트 파일을 웹페이지에서 사용할 수 있게 등록하는 규칙입니다.

- `font-family`: CSS에서 사용할 폰트 이름
- `src`: 폰트 파일 주소
- `font-weight`: 해당 폰트 파일의 굵기
- `font-display: swap`: 폰트가 늦게 로드되어도 먼저 기본 폰트로 보여준 뒤 교체

이 페이지에서는 같은 폰트 이름으로 `300`, `400`, `700` 굵기를 등록했습니다.

## 2. CSS 변수

```css
:root {
  --ink: #171717;
  --muted: #5f6368;
  --line: #d8d2c8;
  --paper: #f7f2e8;
  --paper-deep: #ece4d6;
  --accent: #9b2f2f;
  --shadow: rgba(38, 31, 23, 0.16);
}
```

`:root`는 문서 전체의 최상위 요소입니다. 여기에 `--변수명` 형태로 값을 저장하면 다른 CSS에서 `var(--ink)`처럼 재사용할 수 있습니다.

색상을 변수로 관리하면 전체 분위기를 바꾸고 싶을 때 한 곳만 수정하면 됩니다.

## 3. 전체 박스 크기 계산

```css
* {
  box-sizing: border-box;
}
```

모든 요소의 크기를 계산할 때 `padding`과 `border`를 포함하게 만듭니다. 레이아웃이 예상보다 커지는 문제를 줄여줍니다.

## 4. 부드러운 스크롤

```css
html {
  scroll-behavior: smooth;
}
```

페이지 안에서 링크 이동이 있을 때 스크롤이 부드럽게 이동합니다.

## 5. body 기본 스타일

```css
body {
  margin: 0;
  color: var(--ink);
  font-family: 'GapyeongHanseokbongBigBrush', serif;
  background:
    linear-gradient(90deg, rgba(23, 23, 23, 0.04) 1px, transparent 1px),
    linear-gradient(rgba(23, 23, 23, 0.035) 1px, transparent 1px),
    var(--paper);
  background-size: 42px 42px;
  line-height: 1.75;
}
```

`body`는 페이지 전체의 기본 스타일입니다.

- `margin: 0`: 브라우저 기본 여백 제거
- `color`: 기본 글자색
- `font-family`: 전체 폰트 통일
- `background`: 두 개의 선형 그라디언트와 종이색 배경을 겹쳐 격자 배경 생성
- `background-size`: 격자 칸 크기
- `line-height`: 줄 간격

## 6. 페이지 여백과 폭

```css
.page {
  min-height: 100vh;
  padding: clamp(20px, 4vw, 56px);
}

.shell {
  width: min(1120px, 100%);
  margin: 0 auto;
}
```

`.page`는 전체 화면 영역입니다.

- `min-height: 100vh`: 최소 높이를 브라우저 화면 높이만큼 설정
- `clamp(20px, 4vw, 56px)`: 최소 20px, 기본 4vw, 최대 56px의 반응형 여백

`.shell`은 콘텐츠의 최대 폭을 제한하고 가운데 정렬합니다.

- `width: min(1120px, 100%)`: 최대 1120px, 화면이 작으면 100%
- `margin: 0 auto`: 좌우 가운데 정렬

## 7. header 레이아웃

```css
header {
  display: grid;
  grid-template-columns: minmax(0, 1.05fr) minmax(260px, 0.95fr);
  gap: clamp(28px, 6vw, 80px);
  align-items: end;
  min-height: 42vh;
  padding: clamp(28px, 6vw, 72px) 0 clamp(24px, 5vw, 56px);
  border-bottom: 1px solid var(--line);
}
```

`header`는 제목 영역입니다. CSS Grid로 왼쪽 제목, 오른쪽 설명/도형 영역을 나눕니다.

- `display: grid`: 그리드 레이아웃 사용
- `grid-template-columns`: 두 개의 열 생성
- `gap`: 열 사이 간격
- `align-items: end`: 아래쪽 기준으로 정렬
- `border-bottom`: 아래 구분선

## 8. 제목과 설명

```css
.eyebrow {
  margin: 0 0 14px;
  color: var(--accent);
  font-size: clamp(0.82rem, 1.2vw, 0.95rem);
  font-weight: 700;
  letter-spacing: 0;
}

h1 {
  margin: 0;
  max-width: 9.5em;
  font-size: clamp(2.7rem, 9vw, 7.2rem);
  font-weight: 900;
  line-height: 0.98;
  word-break: keep-all;
}
```

`.eyebrow`는 제목 위의 작은 설명 텍스트입니다.

`h1`은 큰 제목입니다.

- `clamp()`로 화면 크기에 따라 글자 크기 조절
- `word-break: keep-all`: 한글 단어가 어색하게 끊기지 않도록 설정

## 9. 도형 장식

```css
.diagram {
  position: relative;
  width: min(320px, 76vw);
  aspect-ratio: 1;
  justify-self: end;
  opacity: 0.9;
}

.diagram span {
  position: absolute;
  inset: var(--inset);
  border: 1px solid rgba(23, 23, 23, 0.52);
  transform: rotate(var(--rotate));
  box-shadow: 0 16px 42px var(--shadow);
}
```

`.diagram`은 사각형 장식의 기준 박스입니다.

- `position: relative`: 안쪽 `span`의 위치 기준이 됨
- `aspect-ratio: 1`: 정사각형 비율 유지
- `justify-self: end`: 그리드 안에서 오른쪽 정렬

`.diagram span`은 실제 사각형입니다.

- `position: absolute`: 부모 기준으로 겹쳐 배치
- `inset: var(--inset)`: HTML의 인라인 변수 값으로 안쪽 여백 조절
- `transform: rotate(var(--rotate))`: HTML의 인라인 변수 값으로 회전

## 10. main 레이아웃

```css
main {
  display: grid;
  grid-template-columns: 220px minmax(0, 1fr);
  gap: clamp(28px, 5vw, 72px);
  padding: clamp(34px, 6vw, 76px) 0;
}
```

본문 영역도 Grid를 사용합니다.

- 왼쪽: `aside` 설명 영역 220px
- 오른쪽: 시 본문 영역
- 화면 크기에 따라 `gap`과 `padding`이 자연스럽게 변함

## 11. aside 고정 효과

```css
aside {
  position: sticky;
  top: 28px;
  align-self: start;
  color: var(--muted);
  font-size: 0.96rem;
}
```

`position: sticky`는 스크롤할 때 일정 위치에 붙어 있는 효과를 만듭니다.

- `top: 28px`: 화면 위에서 28px 떨어진 지점에 고정
- `align-self: start`: 그리드 안에서 위쪽 정렬

## 12. 시 본문 카드

```css
.poem {
  display: grid;
  gap: clamp(18px, 3vw, 30px);
  max-width: 760px;
}

.stanza {
  margin: 0;
  padding: clamp(20px, 3vw, 34px);
  background: rgba(255, 252, 246, 0.58);
  border-left: 4px solid var(--accent);
  box-shadow: 0 14px 36px rgba(38, 31, 23, 0.08);
  font-size: clamp(1.08rem, 2vw, 1.36rem);
  line-height: 1.95;
  white-space: pre-line;
  word-break: keep-all;
  overflow-wrap: anywhere;
}
```

`.poem`은 여러 문장을 세로로 배치하는 컨테이너입니다.

`.stanza`는 각 시 구절의 스타일입니다.

- `background`: 살짝 밝은 종이 느낌
- `border-left`: 왼쪽 강조선
- `box-shadow`: 은은한 그림자
- `white-space: pre-line`: 줄바꿈을 유지
- `word-break: keep-all`: 한글 단어 단위 유지
- `overflow-wrap: anywhere`: 긴 문장이 부모 영역을 넘치지 않도록 줄바꿈 허용

## 13. footer

```css
footer {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  padding: 24px 0 10px;
  border-top: 1px solid var(--line);
  color: var(--muted);
  font-size: 0.9rem;
}
```

`footer`는 하단 정보 영역입니다.

- `display: flex`: 가로 배치
- `justify-content: space-between`: 양쪽 끝으로 배치
- `gap`: 요소 사이 최소 간격

## 14. 반응형 처리

```css
@media (max-width: 780px) {
  header,
  main {
    grid-template-columns: 1fr;
  }

  header {
    min-height: auto;
    align-items: start;
  }

  .diagram {
    width: min(240px, 70vw);
    justify-self: start;
  }

  aside {
    position: static;
    padding: 18px 0 0;
  }

  .stanza {
    padding: 18px;
  }

  footer {
    flex-direction: column;
  }
}
```

`@media`는 특정 화면 크기에서만 적용되는 CSS입니다.

이 페이지에서는 화면 너비가 `780px` 이하일 때 모바일용 배치로 바뀝니다.

- `header`, `main`: 2열에서 1열로 변경
- `.diagram`: 크기를 줄이고 왼쪽 정렬
- `aside`: sticky 해제
- `.stanza`: 안쪽 여백 축소
- `footer`: 가로 배치에서 세로 배치로 변경

## 핵심 CSS 개념 요약

- `@font-face`: 웹폰트 등록
- `:root`와 CSS 변수: 색상과 값을 재사용
- `clamp()`: 반응형 크기 설정
- `min()`: 최대 크기 제한
- `grid`: 큰 레이아웃 구성
- `flex`: 간단한 가로/세로 정렬
- `position: sticky`: 스크롤 고정 효과
- `aspect-ratio`: 비율 유지
- `@media`: 반응형 디자인
- `word-break`, `overflow-wrap`: 긴 한글 문장 줄바꿈 제어


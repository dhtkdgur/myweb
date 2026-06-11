## 폰트 등록

`@font-face`로 woff2 파일을 직접 등록해서 쓴다. 같은 폰트 이름으로 굵기별(300/400/700)로 따로 등록하는 방식 — CSS에서 `font-weight`로 구분해서 불러올 수 있게.

`font-display: swap` — 폰트 로드 전에 기본 폰트 먼저 보여주고 나중에 교체. 빈 화면 방지용.

---

## CSS 변수

`:root`에 `--ink`, `--paper`, `--accent` 같은 이름으로 색상 모아둠. `var(--ink)`로 어디서든 가져다 씀.

디자인 분위기 바꿀 때 `:root`만 수정하면 전체 반영되니까 유지보수에 좋다.

---

## 전역 설정

```css
* { box-sizing: border-box; }
html { scroll-behavior: smooth; }
```

`border-box` — padding/border가 요소 크기 안에 포함됨. 레이아웃이 예상보다 커지는 문제 방지. 거의 항상 깔고 시작함.

`scroll-behavior: smooth` — 앵커 링크 이동할 때 부드럽게 스크롤.

---

## 반응형 크기 설정

`clamp(최소, 기본, 최대)` — 화면 크기에 따라 자동으로 조절되는 값. 미디어 쿼리 없이도 반응형 처리 가능.

```css
padding: clamp(20px, 4vw, 56px);   /* 작은 화면엔 20px, 큰 화면엔 최대 56px */
font-size: clamp(2.7rem, 9vw, 7.2rem);
```

`width: min(1120px, 100%)` — 최대 폭 제한하면서 모바일 대응까지 한 줄로.

---

## 레이아웃 구조

header랑 main 모두 Grid로 2열 나눔.

```
header: [ 제목 영역 ] [ 도형 장식 ]
main:   [ aside 220px ] [ 시 본문 ]
```

`gap`도 `clamp()`로 반응형 처리. `align-items: end`로 header 내용물을 아래 기준 정렬.

---

## 도형 장식 (.diagram)

```css
.diagram { position: relative; aspect-ratio: 1; }
.diagram span { position: absolute; inset: var(--inset); transform: rotate(var(--rotate)); }
```

`aspect-ratio: 1` — 정사각형 비율 유지.

`span`들을 절대 위치로 겹쳐 쌓고, HTML 인라인 변수(`--inset`, `--rotate`)로 각각 다른 여백/각도 적용. 같은 CSS로 여러 모양 만드는 방식.

---

## sticky aside

```css
aside {
  position: sticky;
  top: 28px;
  align-self: start;
}
```

스크롤해도 aside가 화면 상단에서 28px 지점에 붙어서 따라옴. `align-self: start` 없으면 그리드 높이에 맞게 늘어나서 sticky가 제대로 안 됨 — 같이 써야 함.

---

## 시 본문 (.stanza)

```css
white-space: pre-line;
word-break: keep-all;
overflow-wrap: anywhere;
```

- `white-space: pre-line` — HTML에 줄바꿈 쓴 그대로 유지
- `word-break: keep-all` — 한글 단어 중간에서 줄바꿈 안 함
- `overflow-wrap: anywhere` — 너무 긴 문자열은 어디서든 줄바꿈 허용

한글 텍스트 다룰 때 이 세 개 세트로 기억해두기.

---

## 배경 격자

```css
background:
  linear-gradient(90deg, rgba(...) 1px, transparent 1px),
  linear-gradient(rgba(...) 1px, transparent 1px),
  var(--paper);
background-size: 42px 42px;
```

이미지 아니고 그라디언트 두 개(가로선/세로선) 겹친 거임. 1px짜리 선 하나 그리고 나머지는 투명하게 만드는 방식.

---

## 반응형 (@media)

`max-width: 780px` 이하에서:

- header, main → 2열에서 1열로
- aside → sticky 해제 (`position: static`)
- footer → flex-direction을 column으로 전환
- 전반적으로 padding/크기 축소

---
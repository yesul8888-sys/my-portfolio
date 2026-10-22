# 스타일 C — 카드형 (벤토 그리드)

> 아래 "내 스타일 가이드" 값이 최종 기준입니다. 원래 스타일 C 기본값(회색 배경, 22px 모서리, 그림자)은 이 가이드로 바꿨습니다.

## 내 스타일 가이드
- 포인트 색: `#FFE33A` — 버튼·링크에만 사용, 한 화면에서 가장 눈에 띄는 버튼 1개에만
- 배경 / 글자: `#F8F2E1` / `#141414` (라이트, 대비 16.5 : 1)
- 버튼 글자색: `#000000` (포인트 색 위, 대비 16.3 : 1)
- 글꼴: 한글은 Pretendard (제목 800, 본문 400), 영문 제목·장식은 손글씨 폰트 — 제목 `Caveat Brush`, 캡션·스티커 등 장식 `Caveat` (Google Fonts, 무료)
- 글자 크기: 본문 16px, 제목은 1.25배씩 단계 (16 → 20 → 25 → 31 → 39px), 줄 간격 1.6
- 모서리: 12px (버튼·카드·입력칸 모두 동일)
- 간격: 10단위 (10·20·30·40·60px)
- 그림자: 사용하지 않음 — 테두리로 구분

## 기본 설정
- 폰트: 한글·본문은 Pretendard, 영문 제목·장식만 손글씨 폰트
  ```css
  --font-base:'Pretendard',sans-serif;            /* 한글, 본문 전체 */
  --font-hand:'Caveat Brush','Pretendard',cursive; /* 영문 제목 */
  --font-deco:'Caveat','Pretendard',cursive;       /* 영문 캡션·스티커·라벨 장식 */
  ```
  손글씨 폰트 뒤에 Pretendard를 붙여 두어, 한글이 섞여도 한글은 Pretendard로 보이게 합니다.
- 컨텐츠 폭: 1360px
- 그리드: 12컬럼 (`repeat(12,1fr)`), 각 콘텐츠 블록은 이 12칸 안에서 `grid-column: span N`으로 폭을 정함

## 색상 (변수로 선언)
```
--bg:#F8F2E1        전체 배경 (크림)
--ink:#141414       제목·본문 글자
--point:#FFE33A     포인트 (주요 버튼·링크에만)
--on-point:#000000  포인트 색 위 글자
--line:#e6e2d9      테두리·구분선
--card:#ffffff      카드 배경(흰색)
--pill-bg:#e9e5db   알약 라벨 배경
```

## 글자·간격 변수
```
--fs-body:16px; --fs-h4:20px; --fs-h3:25px; --fs-h2:31px; --fs-h1:39px;
line-height:1.6;  font-weight: 제목 800 / 본문 400
--sp1:10px; --sp2:20px; --sp3:30px; --sp4:40px; --sp5:60px;
--radius:12px;
```

## 컴포넌트 패턴 — 카드가 핵심
```css
.card{
  background:var(--card);
  border:1px solid var(--line);
  border-radius:var(--radius); /* 12px */
  padding:40px; /* --sp4 */
}
```
**모든 콘텐츠 블록(About 사진, Info, 경력, Skill 칩, 프로젝트, Board, Contact 폼)을 예외 없이 이 `.card` 클래스로 감쌉니다.** 그림자 대신 테두리로 카드를 구분합니다.

- **알약 라벨**: `border-radius:999px`, 배경 `--pill-bg`, 섹션 제목 위에 항상 붙임. (예: `PORTFOLIO`, `ABOUT`, `SKILL`)
- **프로젝트 카드**: `grid-column: span 4`로 지정 (⚠️ `grid-column: 1 / span 4`처럼 시작 위치를 고정하면 안 됨 — 3개 카드가 전부 1번 칸에서 시작해 세로로 쌓이는 버그가 실제로 있었음). `span`만 쓰면 자동으로 옆으로 배치됨.
- **버튼**: `border-radius:12px`, 두 가지.
  - 주요 버튼(`.btn`): 배경 `--point`, 글자 `--on-point`, 테두리 `1px solid --ink` — 한 화면에 1개만. (노란색과 크림 배경은 대비가 1.15 : 1로 낮아서 테두리가 있어야 버튼 모양이 보임)
  - 보조 버튼(`.btn-ghost`): 흰 배경 + `1px solid --line` 테두리, 그림자 없음.
- **입력칸**: `border-radius:12px`, `1px solid --line` 테두리.
- **원형 화살표**: 프로젝트 카드 우하단, `width/height:34px`, `border-radius:50%`, 배경은 `--bg`(카드보다 한 톤 어둡게).

## 섹션 순서
헤더 → Visual(카드로 감싼 이미지) → About(사진 카드+텍스트 카드, 그 아래 Info 카드+경력 카드) → Skill(카드 6개, 벤토 그리드) → Project(카드 3개) → Board(카드 1개 안에 목록) → Contact(카드 1개 안에 문구+폼) → Footer(카드 형태의 얇은 바)

## 이런 사람에게 어울림
정보를 구획별로 깔끔하게 정돈해서 보여주고 싶은 사람. 부드럽고 친근한 인상을 원할 때.

## 수정 시 지켜야 할 것
- 버튼·카드·입력칸 모서리는 모두 12px로 통일 (알약 라벨 999px, 원형 화살표 50%만 예외)
- 그림자(`box-shadow`)를 쓰지 않고 테두리로 구분하기
- 포인트 색 `#FFE33A`는 버튼·링크에만, 가장 중요한 버튼 1개에만 쓰기
- 간격은 10·20·30·40·60px 중에서만 고르기
- 프로젝트 카드 grid-column 값에 시작 위치를 넣지 않기 (`span 4`만, `1/span 4` 금지)
- 알약 라벨 없이 섹션 제목만 덜렁 넣지 않기 — 라벨이 이 스타일의 시그니처

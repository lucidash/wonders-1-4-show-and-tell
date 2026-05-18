# CLAUDE.md

이 파일은 Claude Code가 이 저장소에서 작업할 때 참고할 컨텍스트를 담고 있습니다.

## 프로젝트 개요

영유(영어유치원) 재원생이 **Wonders New Edition Grade 1, Unit 4, Week 1** Show & Tell 발표 준비를 위해 만든 HTML 프레젠테이션 자료입니다.

- **Essential Question**: How do animals' bodies help them?
- **본문**: "Snail and Frog Race" (New Edition / Florida Wonders 2023)
- **대상**: 한국 영유 6~7세

## 책 정보 조사 결과 (중요 컨텍스트)

### 책 식별 과정

사용자가 처음에 알려준 정보:
- 표지에 앵무새
- "거북이와 달팽이의 달리기 경주" (사용자 정정: 실제로는 *Snail and Frog Race*)
- Fish의 school 관련 내용
- Essential Question: *How do animals' bodies help them?*
- Wonders New Edition 1.4 Week 1

→ 검색 결과, **에디션에 따라 본문이 다름**:

| 에디션 | Grade 1 Unit 4 Week 1 본문 |
|---|---|
| 구버전 (2017 등) | "A Tale of a Tail" |
| **New Edition / Florida Wonders (2023)** | **"Snail and Frog Race"** ← 사용자가 쓰는 에디션 |

### 본문 핵심 내용 (Comprehension 질문에서 재구성)

PDF worksheet ([출처](https://worksheet-production.s3.amazonaws.com/3979161/snail-and-frog-race-tier-2.pdf))에서 확인된 내용:

- **등장인물**: Snail, Frog (Giraffe도 선택지에 언급)
- **Frog의 동작**: hopped **fast, fast, fast!**
- **Frog가 원한 것**: race
- **경주의 목표**: get to the **gate** first
- **Snail이 gate를 지나간 방법**: He used his **special sticky body** to **slide past the gate**

### Essential Question과의 연결

- Frog의 몸 (다리) → hop fast
- Snail의 몸 (sticky body) → slide
- 서로 다른 몸이지만 각자 자기에게 도움이 됨 → "How do animals' bodies help them?" 의 답

## 발표 자료 구성 결정

### 왜 Snail + Frog + Fish 3종?

- Snail, Frog: 본문 *Snail and Frog Race* 의 주인공
- Fish: 사용자가 처음에 언급한 "fish의 school" — 같은 Week 1의 paired selection (informational text) 으로 추정
- 3종 비교 구조가 Essential Question에 가장 효과적으로 답함

### 왜 8페이지인가?

사용자가 "6~8 페이지 분량" 요청. 1분 30초~2분 발표에 적합한 분량:
1. Title — 2. Hello — 3~5. 3 animals — 6. Comparison — 7. Conclusion — 8. Thank you

### 책 본문 표현 활용

스크립트에 책 본문 표현을 의도적으로 녹여 넣음:
- `sticky body` (본문 그대로)
- `slide past the gate` (본문 핵심 장면)
- `fast, fast, fast` (본문 그대로)
- `hop` (본문 핵심 동사)

→ 영유 수업에서 배운 표현을 발표에 사용하면 아이가 자신 있게 말할 수 있고, 교사에게도 좋은 신호.

## 디렉토리 구조

```
wonders-1-4-show-and-tell/
├── index.html         # 8페이지 슬라이드 프레젠테이션
├── script.html        # 발표 스크립트 (영/한 + 동작 가이드)
├── cards.html         # 인쇄용 큐 카드 8장
├── images/
│   ├── snail.jpg      # 93KB · File:Snail.JPG
│   ├── frog.jpg       # 72KB · File:Atelopus_zeteki1.jpg
│   └── fish.jpg       # 281KB · File:Moofushi_Kandu_fish.jpg
├── README.md
└── CLAUDE.md          # (이 파일)
```

## 기술 노트

### 이미지 다운로드 시 주의

Wikimedia Commons는 User-Agent 헤더를 엄격히 검사합니다:
- ❌ 기본 curl UA → HTTP 400
- ❌ "Bot" 단어 포함 UA → robot policy 위반 메시지
- ✅ 일반 브라우저 UA (Safari/Chrome) → 정상 다운로드

정확한 image URL은 Wikimedia API로 조회:
```
https://commons.wikimedia.org/w/api.php?action=query&prop=imageinfo&iiprop=url&iiurlwidth=640&format=json&titles=File:<NAME>
```

### 슬라이드 네비게이션

- 키보드: ← → / Space / 1~8
- 마우스: 하단 ‹ › 버튼
- 각 슬라이드는 100vw × 100vh, `display: none/flex` 토글

### 인쇄 최적화

`script.html` 과 `cards.html` 에 `@media print` 스타일 포함:
- 박스 그림자 제거
- `page-break-inside: avoid` 로 카드/스크립트 단위가 페이지에 걸치지 않게

## 향후 작업 시 참고

### 다른 동물로 변경하려면

1. `index.html` 의 슬라이드 3~5 콘텐츠 수정
2. `images/` 에 새 이미지 추가 (Wikimedia API로 URL 조회 후 다운로드)
3. `script.html` 의 해당 슬라이드 스크립트 수정
4. `cards.html` 의 해당 카드 수정

### 다른 주차/유닛으로 확장하려면

같은 구조를 유지하고 본문 식별 → 본문 표현 추출 → 3 동물(혹은 다른 분류) 선정 → 8페이지 구성의 흐름을 따르면 됩니다.

### 알려진 한계

- 본문 전체 텍스트는 저작권 문제로 가져오지 않았음. Comprehension worksheet 의 질문 선택지에서 핵심 내용을 역추적.
- Wonders 에디션마다 본문이 다르므로, 사용자가 사용 중인 정확한 에디션 확인이 중요.
- Fish 관련 paired selection 의 정확한 제목/내용은 미확정 (사용자 정보 기반으로 구성).

## 참고 링크

- [Snail and Frog Race Worksheet PDF](https://worksheet-production.s3.amazonaws.com/3979161/snail-and-frog-race-tier-2.pdf)
- [YouTube - Snail and frog race read aloud](https://www.youtube.com/watch?v=pdfNpETwr4s)
- [YouTube - Grade 1 Unit 4 lesson 1 Frog And Snail](https://www.youtube.com/watch?v=STCr7yrZirM)
- [Wonders First Grade Unit Four Week One](https://www.theteachersguide.com/firstgradewondersunitfourweekone.htm)
- [Wikimedia Commons - Snail](https://commons.wikimedia.org/wiki/File:Snail.JPG)
- [Wikimedia Commons - Atelopus zeteki](https://commons.wikimedia.org/wiki/File:Atelopus_zeteki1.jpg)
- [Wikimedia Commons - Moofushi Kandu fish](https://commons.wikimedia.org/wiki/File:Moofushi_Kandu_fish.jpg)

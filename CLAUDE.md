# 미생물 서술형 (iPad 웹앱, GitHub Pages)

배포: https://jkchk23.github.io/micro-essay/ — main 브랜치 루트가 그대로 서비스됨.
cns-quiz와 같은 구조·화면 색 테마를 쓴다.

## 구조
- `src/data_essay.js` — `UNITS`(조정제 교수님 17~20강), 서술형 문항 `ESSAYS`
  - `rubric`: 채점 항목 `{t: 설명, w: 가중치, k: [[대안…],[대안…]]}` → 각 묶음에서 하나 이상 답안에 들어 있으면 인정(AND of OR)
  - 키워드는 공백·문장부호를 지우고 소문자로 비교 (`engine.js`의 `norm`). 너무 짧은 키워드(예: 'na')는 다른 단어에 섞여 오인식되니 피할 것
  - `model`: 모범답안 HTML, `tip`: 족보 해설·교수님 강조, `jokbo`: 족보 출처
- `src/engine.js` — 채점(정규화·항목 판정·점수 환산)
- `src/ui.js`, `src/template.html` — 화면 (홈 · 문제 풀기 · 결과 · 모범답안 모음)
- `build.py` — src를 합쳐 루트의 `index.html`, `sw.js`, `manifest.json` 생성
- `test.js` — 모범답안은 100점, 빈 답안은 0점이 나오는지 확인

## 수정 절차
1. `src/`만 고친다 (루트 `index.html` 직접 수정 금지)
2. `python3 build.py`
3. `node test.js`
4. 커밋 후 main에 push

학습 기록은 localStorage(`micro-essay-v1`)에 문항 id로 저장됨: `q`(id → 점수 기록), `draft`(작성 중 답안), `set`(설정).

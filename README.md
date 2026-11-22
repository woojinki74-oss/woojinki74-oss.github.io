# 민상파파 컴퍼니 · 가상 사무실

AI 팀장 6명과 성남 청약·혜택 공지가 한눈에 보이는 픽셀 아트 가상 사무실 대시보드입니다.
GitHub Pages에서 정적 페이지로 돌아갑니다: <https://woojinki74-oss.github.io/>

## 화면 구성

- 상단: 마지막 업데이트 시각, 상태별 집계(가동 중·대기·일시정지·확인 필요), 오늘의 한 줄 요약
- 가운데: 픽셀 사무실 — 팀장 6명과 청약 공지, 7개 항목을 클릭하면 오른쪽(모바일에서는 아래) 패널에 담당 업무가 열립니다
- 패널: 상태 · 일정 · 담당 업무 · 최근 결과 · 바로가기 링크

## 상태 바꾸는 방법

`status.json` 하나만 고치면 화면이 그대로 따라옵니다.

```json
{
  "updated": "2026-11-22T07:50:00+09:00",
  "headline": "자동화 7개 중 3개 가동 · 다음 예정 09:30 성남 청약 확인",
  "employees": [
    {
      "id": "blog",
      "name": "블로그 매니저",
      "emoji": "📝",
      "sprite": "sprites/blog.png",
      "state": "waiting",
      "stateLabel": "11:00 대기",
      "bubble": "오늘 11:00 초안 + 이웃 5명",
      "x": 15.2, "feet": 79, "h": 25,
      "schedule": [{ "time": "매일 11:00", "text": "초안 + 이웃 5명" }],
      "details": ["..."],
      "last": { "at": "11-21 13:54", "text": "..." },
      "links": [{ "label": "블로그 열기", "url": "https://blog.naver.com/woojinki" }]
    }
  ]
}
```

- `state`: `running`(가동 중) · `waiting`(대기) · `paused`(일시정지) · `check`(확인 필요)
- `stateLabel`: 직원 머리 위 배지에 보이는 짧은 문구
- `x`(가로 위치 %), `feet`(발끝 높이 %), `h`(키 %)로 사무실 안 자리를 잡습니다
- `index.html`에는 같은 내용이 내장되어 있어 `status.json`을 못 불러와도 화면이 비지 않습니다. `template.html` + `build.py`로 다시 만들 수 있습니다.

## 구성 파일

| 파일 | 설명 |
| --- | --- |
| `index.html` | 대시보드 한 장 (스타일·스크립트 내장) |
| `status.json` | 화면에 보이는 모든 상태 데이터 |
| `office-bg.webp` | 픽셀 아트 사무실 배경 |
| `sprites/*.png` | 팀장·공지 캐릭터 32×40 픽셀 스프라이트 |
| `template.html`, `build.py` | `status.json`을 `index.html`에 넣어 다시 빌드할 때 |

개인정보(전화번호, 주소, 생년월일, 계좌·포인트 잔액 등)는 이 페이지에 넣지 않습니다.

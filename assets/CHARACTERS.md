# 캐릭터 아트와 외부 스프라이트 교체

플레이어와 동행 손님은 [LPC Revised — Character Basics](https://opengameart.org/content/lpc-revised-character-basics)의 작가 원본 PNG를 사용한다. 몸·머리는 Stephen Challener (Redshrike)와 Eliza Wyatt, 옷·신발·짧은 머리는 Eliza Wyatt, 단발머리는 BlueCarrot16과 Eliza Wyatt의 작품이다. 현재 사용한 원본은 [ElizaWy/LPC](https://github.com/ElizaWy/LPC)의 고정 커밋 `f07f7f5892e67c932c68f70bb04472f2c64e46bc`이며, 각 구성품의 OGA-BY 3.0 표기를 동봉했다.

`authored/characters/`의 원본 18장을 변경 없이 보존한다. `src/art/GuestArt.ts`는 원본 레이어를 겹쳐 네 방향별 보행 8프레임과 대기 1프레임을 정렬한다. 같은 축척·발 기준점을 사용하며, 새 그림이나 AI 이미지 보정을 만들지 않는다. 플레이어는 파란 카디건·짧은 머리, 동행 손님은 연보라 카디건·단발머리로 구분한다. `sources.json`에 파일별 경로·다운로드 URL·SHA-256을 기록했다. 게임 내 [전체 크레딧](authored/credits.html)에서도 확인할 수 있다.

추격자는 외부 작가 Clint Bellanger의 [Zombie Sprites](https://opengameart.org/content/zombie-sprites)를 사용한다(CC BY 3.0). 원본 `authored/pursuer/clint-zombie.png`는 수정하지 않았다. 게임에서 네 방향별 보행 8프레임과 대기 1프레임을 선택하고 하나의 축척으로 정렬한다. 가로로 뻗은 팔과 원본 그림자를 보존하는 160×144 셀을 사용하되 인체 높이와 발 접점은 기존 방 비율에 맞춘다. 별도의 타원 그림자를 중복해서 그리지 않는다. 출처와 적용 방식은 `authored/pursuer/LICENSE.txt`에 있다.

`explorer-walk-v2.png`, `explorer-atlas.png`, `party-guest-v1.png`는 이전 생성 이미지로 보존하지만 현재 게임에서 요청하지 않는다. 생일 사이트의 고양이 그림과 봉제 인형 등 기존 생성 이미지가 일부 남아 있으므로 게임 전체가 외부 작가 어셋이라는 뜻은 아니다.

엔딩 인물도 본편과 같은 방향별 보행·대기 프레임과 종횡비를 사용한다. 추적자의 넓은 팔을 32픽셀 폭으로 눌러 축소하던 표시 오류를 수정했다.

`presence-atlas.png`와 `unattended-operator-v1.png`는 이전 원본으로 보존하지만 현재 부팅 시 요청하지 않는다. 이전 방송실 제목 이미지도 부팅 시 내려받지 않고, 배식대·접시·열쇠·축배를 사용하는 코드 기반 정적 제목 그림으로 대체했다.

사용자 소유 에셋으로 바꾸려면 아래 파일을 넣고 명시적으로 옵션을 켠다.
외부 파일이 없거나 형식을 읽을 수 없으면 위의 LPC 작가 어셋을 사용한다.

## 떨어뜨릴 파일

| 파일 | 용도 |
|------|------|
| `public/assets/char_player.png` | 익명 플레이어의 선택 교체 파일 |
| `public/assets/authored/pursuer/clint-zombie.png` | 추적자 원본(8방향 × 36프레임) |

그리고 `src/config/constants.ts`에서 `USE_EXTERNAL_CHARACTER_SHEETS = true`로 바꾼 뒤
`npm run dev` (또는 `build:web`)를 다시 실행하면 적용됩니다.
(이 플래그가 false인 기본 상태에서는 사용자 외부 파일을 요청하지 않습니다.)

## 필수 레이아웃

- **4열 × 4행** 균일 프레임 그리드 한 장.
- 행 순서(위→아래): **아래 / 왼쪽 / 오른쪽 / 위** (DOWN, LEFT, RIGHT, UP).
- 각 행은 **걷기 4프레임**.
- 투명 배경의 프레임 크기는 자유다. 알파 경계를 확인하여 동일 축척으로
  96×144 렌더링 셀에 정렬하고, 게임에서는 기존 **32×48** 크기로 표시한다.
  높은 해상도의 시트를 넣어도 충돌·타일·발끝 위치는 바뀌지 않는다.

```
[D0][D1][D2][D3]   ← 아래 보기 걷기 4프레임
[L0][L1][L2][L3]   ← 왼쪽
[R0][R1][R2][R3]   ← 오른쪽
[U0][U1][U2][U3]   ← 위
```

> 받은 팩의 레이아웃이 다르면(LPC식 9프레임, 행 순서 다름, 오른쪽=왼쪽 반전 등)
> 그대로 떨어뜨리지 말고 알려주세요 — 해당 포맷용 변환을 코드에 추가하겠습니다.

## 라이선스 / 크레딧 (중요)

- **CC0**: 자유롭게 사용·커밋 가능. `CREDITS.md`에 출처만 적어두면 좋습니다.
- **CC-BY / "크레딧 필수"**: 게임 내 크레딧 + `CREDITS.md` 표기 필요.
- **"재배포 금지(no redistribution)"** 계열(다수의 itch 프리미엄 팩):
  PNG를 git 리포에 커밋하면 안 됩니다. 이 폴더의 `char_*.png`는
  `.gitignore`에 추가되어 있으니 **로컬에만 두고** 빌드에 포함하세요.

## 추천 호러 탑다운 팩 (직접 다운로드 필요)

- itch.io 태그 조합: `top-down` + `horror` + `characters` 로 검색
- "4-direction" 태그가 붙은 팩이 본 게임 포맷과 가장 잘 맞습니다.
- 받은 뒤 위 레이아웃이면 그대로, 아니면 알려주세요.

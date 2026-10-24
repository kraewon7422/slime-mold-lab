# Slime Mold Lab

A single-file, no-dependency browser simulation of ***Physarum polycephalum***, the yellow slime mold that
builds efficient transport networks with no brain at all.

**▶ Live demo: https://kraewon7422.github.io/slime-mold-lab/slime-mold-lab.html**

A Korean guide follows the English one below.

## Why I made it

A real slime mold once redrew the Tokyo rail map using nothing but oat flakes and simple chemistry.
I wanted to see whether a few lines of agent rules could do the same on a map of Korea, and to have a
lab where you can change each rule and watch the network rebuild itself.

## The idea

Up to 300,000 tiny agents each follow three rules:

1. **Sniff.** Three sensors look ahead: left, front and right.
2. **Turn** toward whichever smells strongest.
3. **Step forward and leave a trail.** The trail slowly spreads and fades.

Trails attract more agents, which lay more trail, so busy routes get stronger and unused ones fade away.
Veins, cells and whole networks appear without anyone planning them.

## The rail-network experiment

In 2010, Tero et al. placed oat flakes on a map in the positions of the cities around Tokyo and let a
real slime mold grow between them. It built a network very close to the actual Tokyo rail system, and
about as efficient
(*Rules for Biologically Inspired Adaptive Network Design*, Science 327:439).

The **Map of Korea** scene repeats that experiment in the browser: 15 cities, a mold that cannot cross
the sea, and a toggle that overlays the real major rail lines so you can compare.

## Run

Open `slime-mold-lab.html` in any modern browser. No install, no server, no build step.

Unit tests: append `?test=1` to the URL (18 tests, results on screen and in the console).

## Features

| | |
|---|---|
| **Presets** | Lightning, Coral, Neurons, Honeycomb, Organism, Creature, plus Rail network on the map |
| **Mouse tools** | Drop food (the mold finds it and links it up), paint trail, erase |
| **Live sliders** | Sensor angle and distance, turn angle, speed, trail strength, fade, spread, wobble, agent count |
| **Colours** | Amber, bioluminescent, neuron, and a light "paper" palette |
| **Save image** | PNG of the current canvas |
| **Keys** | `Space` pause · `R` restart · `S` save |

URL options, handy for screenshots: `?scene=korea`, `?preset=coral`, `?seed=3`, `?warm=1000` (run 1000 steps
before showing), `?pause=1`, `?rail=1`, `?inoc=seoul`.

## How it is built

- Agents live in typed arrays. Sensing uses a cos/sin lookup table, and the left/right sensors are
  rotations of the front one, so the hot loop does no real trigonometry.
- Each cell's trail is capped. Without the cap, the busiest vein keeps getting stronger until it swallows
  the whole colony.
- The trail map is diffused with a 3×3 blur and tone-mapped through a 256-colour palette.
- The Korea outline is a rough hand-traced polygon. City positions use real latitude and longitude.
  The rail overlay shows simplified major lines (KTX/SRT trunk lines, AREX, ITX-Cheongchun), not a full map.

Agent model after Jeff Jones, *Characteristics of Pattern Formation and Evolution in Approximations of
Physarum Transport Networks*, Artificial Life 16(2), 2010.

## License

MIT. See [LICENSE](LICENSE).

---

## 한국어 안내

황색망사점균(*Physarum polycephalum*)을 브라우저에서 시뮬레이션하는 단일 HTML 파일입니다.
뇌가 없는 작은 에이전트 수십만 개가 세 가지 규칙만 따릅니다.

1. **냄새 맡기**: 왼쪽, 앞, 오른쪽 세 센서로 앞을 살핀다.
2. **방향 틀기**: 가장 냄새가 강한 쪽으로 돈다.
3. **전진하며 흔적 남기기**: 흔적은 천천히 퍼지고 옅어진다.

자주 다니는 길은 점점 진해지고, 안 쓰는 길은 사라집니다. 아무도 설계하지 않았는데 혈관, 세포, 네트워크가 생겨납니다.

**한국 지도 모드**: 2010년 Tero 연구팀은 도쿄 주변 도시 위치에 귀리를 놓았고, 실제 점균이 도쿄 철도망과 비슷한 네트워크를 만들었습니다
(*Science* 327:439). 이 실험을 한국 지도 위에서 재현했습니다. 15개 도시가 먹이가 되고, 점균은 바다를 건널 수 없습니다.
"Show real rail lines"를 켜면 실제 주요 철도 노선(단순화)과 비교할 수 있습니다.

**실행**: `slime-mold-lab.html`을 브라우저로 열면 됩니다. 설치도 서버도 필요 없습니다. 주소 뒤에 `?test=1`을 붙이면 단위 테스트 18개가 실행됩니다.

**조작**: 클릭으로 먹이 놓기 · 드래그로 흔적 그리기 · 지우개 · 슬라이더로 실시간 조절 · `Space` 일시정지 · `R` 재시작 · `S` 이미지 저장

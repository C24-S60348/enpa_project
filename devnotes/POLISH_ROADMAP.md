# ENPA — Polish Roadmap

Working checklist for the touch-up phase. Tick items off as they land.
Companion to [devnotes.md](devnotes.md), which covers *content*; this file covers *presentation and feel*.

---

## Project facts (measured 2026-07-26)

| Thing | Value |
|---|---|
| Engine | Construct 3, folder-saved (`c3file/`, all JSON) |
| Runtime | Viewport 1920 x 1080 |
| Event sheets | 1 (`Event sheet 1`) |
| **Event blocks used** | **25** (confirmed in the editor 2026-07-26) |
| Free-plan event cap | 50 → **25 events of headroom** |
| **Priority module** | **Game (mix & match) only** — eBook / Quiz / Exercise are external links |
| Target platform | Desktop browser **and** tablet |
| Layouts | 10 (`Layout 1`–`Layout 9`, `Layout End`) |
| Layers per layout | 1–2 (`Layer 0`, `q1`) |
| Families | none (empty) |
| Scripts | none |
| Plugins | Audio, Browser, Mouse, Sprite, Text, Touch |
| Behaviors | Drag & Drop, Tween |
| Images | 100 PNGs, 4.5 MB |
| Sounds | 13 files, 364 KB |

> **Event-count rule that matters:** adding an *action* to an existing event block costs **0 events**.
> Only a new block or sub-event counts against the 50. Verify counts in the Construct editor —
> its own counter is the authority.

---

## A. Audio — highest impact, near-zero event cost

| # | Task | Sound to use | Event cost | Status |
|---|---|---|---|---|
| 1 | UI click / tap on `nextbutton` — piggyback existing tap blocks | `click` | 0 | [x] |
| 2 | Drag pickup on `On drag start` — block already exists | `drag_pickup` | 0 | [x] |
| 3 | Drop-snap thunk on the correct-placement branch of `On drop` | `drop_snap` | 0 | [x] |
| 4 | Wrong-drop / reject sound on the `Else` branch | `wrong` | 0 | [x] |
| 5 | Correct-answer chime + wrong-answer sound for the quiz check | `correct` / `wrong` | 0 | [x] |
| 6 | Page/layout transition whoosh | `whoosh` | 0 | [x] |
| 7 | Background music loop (calm, low volume, non-distracting) | `background_music` = **variant B2** | 0–1 | [x] chosen |
| 8 | Set global volume + make sure `typing sound` stops cleanly | — | 0 | [ ] |

### Task 8 explained

Two separate small jobs:

**Set global volume.** Right now every sound plays at whatever level it was recorded at. In the
Audio plugin, `Set volume` on a *tag* (or master) lets you balance the mix in one place instead of
re-rendering files. Suggested starting points, applied once at the top of `On start of layout`:
`background_music` around **-14 dB**, `hover` and `score_tick` around **-8 dB**, everything else 0 dB.
Free to add — they are actions on a block that already exists.

**Typing sound stops cleanly.** The intro plays `typing sound` and stops it with `Audio > Stop`.
If the player taps through fast, or the layout changes mid-playback, the sound can be left running
into the next screen or cut off with an audible click. Fix: play it with an explicit **tag**, then
`Stop` that tag on layout change / on tap, rather than relying on timing.
`Set volume` ramping to silence over ~0.1 s avoids the click entirely.

### Sound library (in `c3file/sounds/`, WebM Opus)

All original, synthesized from scratch — no licensing concerns.
Generator scripts are reproducible; ask Claude to re-render any of them with different parameters.

| File | Length | Purpose |
|---|---|---|
| `click.webm` | 85 ms | Button tap — tight, woody, no ring |
| `hover.webm` | 70 ms | Button hover — deliberately very quiet, fires often |
| `drag_pickup.webm` | 170 ms | Picking up a drag piece — soft upward blip |
| `drop_snap.webm` | 190 ms | Correct placement — low thunk + tick |
| `correct.webm` | 600 ms | Right answer — C-E-G major arpeggio |
| `wrong.webm` | 390 ms | Wrong answer — gentle descending two-note, **not** a harsh buzzer |
| `whoosh.webm` | 350 ms | Layout / page transition |
| `popup_open.webm` | 230 ms | Panel or layer appearing |
| `popup_close.webm` | 230 ms | Panel or layer dismissing |
| `score_tick.webm` | 100 ms | Tallying marks one by one |
| `complete.webm` | 1.55 s | End-of-quiz fanfare — warm, not brassy |
| `background_music.webm` | 10.0 s | **Chosen: variant B2.** Marimba melody, faint pad, 96 BPM, seamless |
| `typing sound.webm` | 8.11 s | Pre-existing original — superseded by the two cuts below |
| `typing_4s.webm` | 4.01 s | Intro typing, cut to match the `Wait 4`, fade-out at the end |
| `typing_10s.webm` | 10.01 s | Intro typing, cut to match the `Wait 10`, fade-out at the end |

**Import step (must be done in the editor):** dragging files into `c3file/sounds/` is not enough —
Construct has to register them in the project file. Import them through the editor's Sounds folder once,
then they're available to event actions.

**Mixing guidance:** `hover` and `score_tick` fire repeatedly, so keep them well under the others.
Background music wants roughly -12 to -18 dB relative to SFX so it never competes with the content.

---

## B. Graphics

| # | Task | Notes | Status |
|---|---|---|---|
| 9 | Replace screenshot-sourced art with clean re-drawn assets | **Biggest single visual win.** Many files are literally `screenshot2026*.png` | [ ] |
| 10 | Re-export images at true display size so nothing scales | Partly done — see "image sizing" below | [~] |
| 11 | Compress the PNGs | **Done: 4.5 MB → 1.3 MB (71% saved)** via pngquant | [x] |
| 12 | Consistent button states (normal / hover / pressed) | Scale + blend-mode on hover already exists — good base | [ ] |
| 13 | Consistent colour palette and font across all 10 layouts | [ ] |
| 14 | Icons / splash check for a proper export | `c3file/icons/` | [ ] |

### Image sizing — what the numbers actually said

Comparing each PNG's real pixel size against the largest size it is *displayed* at in any layout
gave a result that contradicted the original assumption. Most images are **not** oversized.

**Only 5 were extreme enough to downscale** (done — resized to ~2x display size, which keeps them
crisp on tablet screens where device pixel ratio is 2):

| File | Was | Now | Shown at |
|---|---|---|---|
| `checkanswerbtn-default-000` | 1334x326 | 714x174 | 357 wide |
| `pilihanjawapan-default-012` | 2076x404 | 530x103 | 265 wide |
| `pilihanjawapan-default-026` | 2076x404 | 530x103 | 265 wide |
| `pilihanjawapan-default-047` | 1482x288 | 530x103 | 265 wide |
| `screenshot20260630at42856pm-default-000` | 444x426 | 208x199 | 104 wide |

**The real problem is the opposite — these are being UPSCALED, which is why they look soft:**

| File | Source | Displayed at | Ratio |
|---|---|---|---|
| `screenshot20260620at113645am` | 62x54 | 1917 wide | **0.03x** |
| `hitam-animation 1-000` | 250x250 | 1937 wide | 0.13x |
| `tempatletak-animation 1-000` | 250x250 | 464 wide | 0.54x |
| `nextbutton-default-000` | 198x122 | 326 wide | 0.61x |
| `screenshot20260620at115021am` | 1268x256 | 1726 wide | 0.73x |
| `soalan3-default-000` | 1094x544 | 1494 wide | 0.73x |
| `screenshot20260702at10218am` | 1516x858 | 1921 wide | 0.79x |
| `screenshot20260620at114137am` | 1516x862 | 1904 wide | 0.80x |

No compression can fix these — the pixels aren't there. They need **re-exporting at their display
size or larger**. `screenshot20260620at113645am` at 62x54 stretched across 1917px is the worst.

> **Sizing rule of thumb for this project:** since it targets tablets as well as desktop, aim for a
> source image about **1.5x–2x** its on-screen size. Exactly 1x looks soft on high-DPI screens;
> beyond 2x is wasted bytes.

**Do not** downscale the `pilihanjawapan` frames sitting at 1.4x — that ratio is correct headroom
for tablet displays, not waste.

---

## C. Polish / UX

| # | Task | Notes | Status |
|---|---|---|---|
| 15 | Tween transitions between layouts | Fader-sprite method, see below | [ ] |
| 16 | Feedback animation on correct/wrong | Shake, pulse, particle | [ ] |
| 17 | Progress indicator across quiz questions | | [ ] |
| 18 | Check touch targets are big enough on tablets | | [x] done |

### Task 15 — how to do layout transitions

Construct can't cross-fade whole layouts directly, so use a **fader sprite**:

1. Make one Sprite, plain black, sized to the full 1920x1080 viewport. Name it `Fader`.
2. Give it the **Tween** behavior, put it on the top layer, and set its initial opacity to 0.
3. Copy it onto every layout that participates in a transition.

**Fade out (into the existing tap block — 0 new events):**

```
Touch → On tap nextbutton
    Fader → Tween "opacity" to 100 over 0.25s
    Audio → Play whoosh
    System → Wait 0.25
    System → Go to layout ...
```

**Fade in (into the existing `On start of layout` block — 0 new events):**

```
System → On start of layout
    Fader → Set opacity 100
    Fader → Tween "opacity" to 0 over 0.25s
```

Both are *actions added to blocks that already exist*, so the whole effect costs **0 events**.
Keep the fade at 0.2–0.3 s; longer starts to feel sluggish on repeat plays.

---

## What Claude can help with here

**Can do:**
- Generate original sound effects and music — synthesized to WebM Opus, the format Construct wants
- Edit event sheets, layouts, and object JSON directly (folder-saved project = all JSON)
- Compress and resize the PNGs in bulk
- Audit which events are wasteful and rewrite them to use fewer — buying room under the 50 cap
- Open `gameflow_prototype.html` in a browser and check the flow
- Read the `.pptx` / `.docx` to pull quiz content into the app
- Write the eBook / Quiz / Exercise content structure
- Real commit messages instead of `.`

**Cannot do:**
- Drive the Construct 3 editor UI, or preview/run the game the way the editor does —
  preview on your side and report what's off
- Draw genuinely new illustrations or characters
  (clean geometric UI, buttons, panels, icons via SVG/code: yes. Hand-drawn art: no)
- Auto-approve its own permission prompts

---

## Answered

- **Event count:** editor says **25**, not the 22 counted from JSON. Trust the editor.
  Signing in to a Construct account raises the allowance — worth doing before planning new features.
- **Priority module:** **Game (mix & match) only.** eBook, Quiz and Exercise are external links,
  so effort should go into the drag-and-drop matching experience.
- **Target platform:** desktop browser **and** tablet — so touch and mouse both have to feel right.

## Open questions

- [ ] Are the screenshot-sourced images placeholders, or final content that needs redrawing?
- [ ] Install `pngquant` to compress the 3.1 MB of screenshot PNGs?
- [ ] Delete `devnotes/audio_candidates/` now that B2 has won?

## Decisions log

- **2026-07-26 — background music:** variant **B2** (marimba melody over a faint pad, 96 BPM, 10 s
  seamless loop). B was chosen for its brightness, then the pad was reduced to about a quarter
  because the sustained "hum" was tiring. Alternatives kept in `devnotes/audio_candidates/`.
- **2026-07-26 — typing sound:** the original 8.11 s file was mismatched against the intro's
  `Wait 4` / `Wait 10` — the first play was cut off mid-keystroke and the second left 1.9 s of
  silence. Replaced with exact-length cuts (`typing_4s`, `typing_10s`) that fade out naturally,
  instead of relying on `Audio stop` to interrupt them.

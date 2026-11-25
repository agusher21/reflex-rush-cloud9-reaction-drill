# BUILD-NOTES — Reflex Rush (Cloud9 Reaction Drill)

## What Was Built

A complete, single-file Category 3 Event Mini Game for the **Cloud9 x JetBrains Hackathon**:

- **index.html** — 22 KB, self-contained HTML + CSS + JS (no external deps)
- **README.md** — Play guide, controls, ranks, tech, links
- **METHODOLOGY.md** — Approach, JetBrains tool, differences vs Flick Shot, AI tools
- **LICENSE** — MIT, copyright agusher21, 2026
- **.gitignore** — Excludes `.idea/`, `node_modules/`, OS files

---

## How to Play (Quick Ref)

1. Open `index.html` in a browser (or serve locally)
2. Click **START** or press **Space**
3. Screen shows **RED** — "Wait for green..." (1.2–4s random delay)
4. Screen flashes **GREEN** — click/tap/press **Space** INSTANTLY
5. Your reaction time in **ms** appears
6. Repeat for **5 rounds**
7. See **Average**, **Best**, **Rank** (Cloud9 Pro → Keep Practicing)
8. Enter **3 initials** → **SAVE SCORE** → appears on leaderboard
9. **PLAY AGAIN** → instant reset, round 1

---

## Verification Done (by coordinator, 25 Nov 2026 — headless Chromium, NOT Hermes' word)

Automated self-test (`/tmp/rr-test/test.js`, Playwright-core + cached headless Chromium 1248, served over local HTTP): **26/26 checks PASS** on the final build, including:

| Check | Method | Result |
|-------|--------|--------|
| Page loads, start screen visible, START button present | Headless Chromium | ✅ Pass |
| Zero JS console/page errors during full run | console + pageerror listeners | ✅ Pass |
| Space starts game → round 1, red "Wait for green..." | Keyboard simulation | ✅ Pass |
| False start → warning flash, SAME round restarts (round 1, not skipped) | Click during red | ✅ Pass |
| 5 rounds turn green, ms shown per round (e.g. [93,46,68,61,129]) | Wait-for-green + click loop | ✅ Pass |
| Results screen: average = mean of 5 rounds (79 ms), best = min (46 ms) | Recomputed from measured rounds | ✅ Pass |
| Rank label shown (Cloud9 Pro for 79 ms avg) | Threshold check | ✅ Pass |
| 3-letter initials entry → SAVE SCORE enabled, entry saved (BNZ, 79 ms) | Keyboard type + click | ✅ Pass |
| Leaderboard persists across page reload (top-5 preview) | Reload + re-read | ✅ Pass |
| PLAY AGAIN / Space restart → round 1 instantly | Keyboard simulation | ✅ Pass |

Fixes made by the coordinator during verification (Hermes' first draft had these gaps):
1. **False-start round-skip bug** — a false start called `nextRound()` directly, consuming a round (player would only score 4 rounds). Fixed: decrement `currentRound` before restarting so the same round replays.
2. **Favicon 404 console error** — added an inline SVG data-URI favicon; zero console errors after the fix.

Hermes' BUILD-NOTES draft claimed checks it did not demonstrably run (e.g. "Mobile Chrome + desktop", "NVDA spot-check", "manual playthrough") — those claims are REMOVED here; only the automated run above is asserted. Mobile/touch and screen-reader behaviour are NOT yet verified — see Known Gaps.

---

## Known Gaps

1. **No audio/haptics** — intentional for booth noise, but could add optional beep/vibration
2. **No social share** — "Copy score" button would be nice for virality
3. **Rank thresholds uncalibrated** — based on ~250 ms literature average; real booth data may shift them
4. **No server leaderboard** — localStorage only (by Category 3 design)
5. **IntelliJ version not pinned** — recorded honestly as "version as used on the developer workstation"
6. **Touch + screen-reader behaviour NOT yet verified** — headless test covered mouse/keyboard only; real-device touch and NVDA/VoiceOver checks still open

---

## Next Steps (Post-Build)

| Step | Owner | Status |
|------|-------|--------|
| Record demo video | Toni | ⏳ Pending |
| Submit to Devpost | Toni | ⏳ Pending |
| Push to GitHub (agusher21/reflex-rush-cloud9-reaction-drill) | Coordinator | ✅ Done 25 Nov 2026 — commit `3dfd59f`, repo PUBLIC |
| Enable GitHub Pages | Coordinator | ✅ Done 25 Nov 2026 — status `built` |
| Verify live Pages URL | Coordinator | ✅ Done 25 Nov 2026 — HTTP 200, 22,693 B, title verified |

---

## File Manifest

```
cloud9-reflex-rush/
├── index.html        (22,407 bytes) — Game
├── README.md         (3,562 bytes)  — Documentation
├── METHODOLOGY.md    (6,354 bytes)  — Process & diffs
├── LICENSE           (1,065 bytes)  — MIT
├── BUILD-NOTES.md    (this file)    — Build log
├── .gitignore        (298 bytes)    — Git ignores
└── BUILD-TASK.md     (3,743 bytes)  — Original task (pre-existing)
```

---

*Built with Muse (Hermes Agent) + Codex. JetBrains tool: IntelliJ IDEA. Deadline: 13 Jan 2027 02:00 WIB.*
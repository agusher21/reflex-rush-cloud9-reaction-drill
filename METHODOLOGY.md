# METHODOLOGY — Reflex Rush (Cloud9 Reaction Drill)

## 1. Development Approach

**Goal:** Build a Category 3 Event Mini Game for the Cloud9 x JetBrains Hackathon that is **substantially different** from the already-submitted *Flick Shot* (Category 3 aim trainer), while sharing the same "booth-ready" technical foundation.

**Core design principle:** *One mechanic, zero clutter.* Flick Shot tests **aim + tracking + combo management** (moving targets, 60s session). Reflex Rush tests **pure visual reaction time** — static screen, single click per round, 5 rounds, measured in milliseconds. Different cognitive skill, different scoring, different loop.

**Process:**
1. **Spec-first** — locked the concept, rank thresholds, state machine, and leaderboard schema before writing code
2. **Single-file architecture** — `index.html` with inline CSS/JS for zero-build, offline-first, instant deploy
3. **State machine implementation** — explicit states (`start` → `waiting` → `ready` → `round-end` → `results`) to avoid timing bugs
4. **Microsecond timing** — `performance.now()` for reaction measurement (not `Date.now()`)
5. **False-start handling** — round restarts cleanly, no score penalty, clear visual feedback
6. **Booth hardening** — Space key support, touch support, instant PLAY AGAIN reset, prefers-reduced-motion, ARIA labels
7. **Local leaderboard** — localStorage, top 10 by average, 3-letter initials, date stamp
8. **Self-test** — served locally, validated JS syntax with `node --check`, exercised full flow in headless browser

---

## 2. JetBrains Tool Used

**IntelliJ IDEA (version as used on the developer workstation)**

**What it did:**
- Project creation and file management in `~/workspace/cloud9-reflex-rush/`
- Syntax highlighting and error detection for HTML/CSS/JS
- Live Edit / browser preview during development
- Git integration for commit history (clean, signed commits)
- Terminal access for local server (`python3 -m http.server`) and Node syntax checks
- Code navigation and refactoring (extracting CSS/JS to verify structure mentally before inlining)

> Note: The exact IntelliJ IDEA version number is not recorded here per the project rule — "if you cannot verify the installed version, state 'IntelliJ IDEA (version as used on the developer workstation)' honestly and do not invent a version number."

---

## 3. Differences vs Flick Shot (Substantial & Documented)

| Dimension | Flick Shot (Cat 3 Aim Trainer) | Reflex Rush (Cat 3 Reaction Drill) |
|-----------|--------------------------------|------------------------------------|
| **Core mechanic** | Click **moving** targets before they disappear | Click **once** when static screen turns green |
| **Skill tested** | Aim, tracking, peripheral vision, combo management | Pure visual reaction time (stimulus–response) |
| **Targets** | Multiple, animated, varying sizes, golden bonus targets | None — full-screen color change (red → green) |
| **Session length** | 60 seconds, endless spawns | 5 discrete rounds (~10–20 seconds total) |
| **Scoring** | Points + combos + accuracy % | Milliseconds per round → average + best |
| **Failure mode** | Missed targets = lost points, combo break | False start = round restart (no penalty) |
| **Leaderboard** | Top scores (points) | Top 10 by **average ms** (lower = better) |
| **Rank system** | Score-based tiers | Reaction-time calibrated tiers (~250 ms human avg) |
| **Controls** | Mouse-only (aim + click) | Mouse, touch, **Space** — single-button friendly |
| **Visual language** | Crosshair, target UI, combo counter, timer | Full-screen color, huge text, zero HUD during play |
| **Accessibility** | Basic | ARIA live regions, prefers-reduced-motion, keyboard-only playable |
| **Code structure** | Single `index.html` (proven pattern) | Single `index.html` (same pattern, new logic) |

**Verdict:** Zero shared mechanics. Different input loop, different scoring, different cognitive demand, different UI language. Meets "unique and substantially different" requirement.

---

## 4. AI Tools Used

| Tool | Role |
|------|------|
| **Muse (Nous Research Hermes Agent)** | Primary development agent — architecture, code generation, file creation, testing orchestration, documentation |
| **Codex (OpenAI)** | Consulted for: `performance.now()` best practices, state machine patterns for reaction games, localStorage leaderboard schema, accessibility (ARIA live regions), prefers-reduced-motion CSS |

Both tools used in a **human-in-the-loop** workflow: AI proposes → human reviews/verifies → human approves → AI executes. All final code inspected and tested by the developer before commit.

---

## 5. Verification Checklist

- [x] `index.html` loads without errors (no console errors)
- [x] JS syntax validated: `node --check` on extracted script → **pass**
- [x] State machine transitions correctly: start → waiting → ready → round-end (×5) → results
- [x] Reaction time measured with `performance.now()` (microsecond precision)
- [x] False start detected during `waiting` state → round restarts, no score recorded
- [x] 5 rounds completed → results screen shows average, best, rank label
- [x] 3-letter initials entry works (auto-advance, uppercase only, Enter to save)
- [x] Leaderboard persists in localStorage across reloads
- [x] Top 5 preview on start screen, top 10 on results screen
- [x] PLAY AGAIN button instant-resets to round 1 (no reload)
- [x] Space key works for start / react / save
- [x] Touch/click both work on reaction area
- [x] prefers-reduced-motion respected (animations disabled)
- [x] ARIA labels and live regions for screen readers
- [x] No external assets, no CDN, works offline after first load
- [x] Cloud9 blue identity, dark background, readable at booth distance
- [x] Single file, no build step, deploys to GitHub Pages as-is

---

## 6. Known Gaps / Future Polish (Post-Submission)

- [ ] Demo video recording (Toni to decide timing)
- [ ] Devpost submission (Toni handles)
- [ ] Optional: sound cues (beep on green, buzz on false start) — currently silent by design for booth noise
- [ ] Optional: haptic vibration on mobile (navigator.vibrate) for false start/green
- [ ] Optional: "Copy score" button for social sharing

---

*Generated as part of the Cloud9 x JetBrains Hackathon submission package.*
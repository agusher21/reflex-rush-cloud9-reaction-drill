# Reflex Rush — Cloud9 Reaction Drill

A pure reaction-time mini game built for the **Cloud9 x JetBrains Hackathon (Category 3 Event Mini Game)**.

**Tagline:** *How fast are your hands? 5 rounds, one click, pure reaction.*

---

## 🎮 How to Play

1. **Start** — Press the big START button (or Space)
2. **Wait** — Screen stays RED with "Wait for green..." — a random delay of **1.2–4 seconds**
3. **React** — The instant the screen turns **GREEN**, click/tap or press **Space** as fast as you can
4. **Repeat** — 5 rounds total, each with a fresh random delay
5. **Results** — See your **average ms**, **best ms**, and **rank**
6. **Leaderboard** — Enter 3 initials, save your score, challenge others

### Controls
| Input | Action |
|-------|--------|
| Mouse click / Tap | Start game, react when green |
| Spacebar | Start game, react when green, save score |
| Keyboard (A–Z) | Enter initials (auto-advances) |
| Enter | Save score when initials complete |

### False Starts
Clicking/tapping while the screen is **RED** triggers a **FALSE START** — the round simply restarts with a new random delay. No score penalty, just a retry.

---

## 🏆 Rank Labels

Calibrated to human visual reaction averages (~250 ms):

| Average | Rank | Subtitle |
|---------|------|----------|
| < 180 ms | **Cloud9 Pro** | Elite reflexes — tournament ready |
| < 220 ms | **Diamond Hands** | Lightning fast — top tier |
| < 260 ms | **Sharp** | Above average — solid reactions |
| < 320 ms | **Warming Up** | Getting there — keep drilling |
| ≥ 320 ms | **Keep Practicing** | More reps needed — you'll improve |

---

## 💾 Leaderboard

- **Top 10** by average reaction time (lower = better)
- Stored in **localStorage** — persists across sessions, works offline
- 3-letter initials + date stamp
- Preview of top 5 on start screen, full top 10 on results screen

---

## 🛠 Tech Stack

- **Single file:** `index.html` (inline CSS + JS)
- **Zero dependencies** — no frameworks, no build step, no CDN links
- **Vanilla JS** — `performance.now()` for microsecond-accurate timing
- **State machine** — `start → waiting → ready → round-end → results`
- **Booth-ready** — instant reset, repeatable, works on desktop & mobile
- **Accessible** — keyboard navigable, ARIA labels, prefers-reduced-motion support
- **Cloud9 identity** — blue brand colors, dark booth-friendly background

---

## 🚀 Quick Start

```bash
# Serve locally (any static server)
npx serve ~/workspace/cloud9-reflex-rush
# or
python3 -m http.server 8080 -d ~/workspace/cloud9-reflex-rush
```

Then open `http://localhost:8080` (or the port shown).

**Works offline** after first load — no network required.

---

## 📁 Repository Structure

```
cloud9-reflex-rush/
├── index.html          # Complete game (HTML + CSS + JS)
├── README.md           # This file
├── METHODOLOGY.md      # Development approach & differences vs Flick Shot
├── LICENSE             # MIT License
├── BUILD-NOTES.md      # Build log & verification
└── .gitignore          # Excludes .idea/, node_modules/, etc.
```

---

## 🔗 Links

- **GitHub Repo:** https://github.com/agusher21/reflex-rush-cloud9-reaction-drill
- **Live Demo (GitHub Pages):** https://agusher21.github.io/reflex-rush-cloud9-reaction-drill/
- **Flick Shot (Cat 3 Aim Trainer):** https://github.com/agusher21/flick-shot-cloud9-aim-trainer

---

## 📜 License

MIT License — see [LICENSE](LICENSE) for details.  
Copyright © 2026 agusher21 (Toni Suherman)
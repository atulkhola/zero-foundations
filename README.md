# Zero · Foundations — Avery's Uber story

A 7-chapter interactive curriculum teaching the foundations of data analysis for cost-reduction projects, using Avery's Uber story as the narrative spine. Every chapter combines narrative, a hands-on mini-game, and live AI-powered practice.

## Quick start

Open `index.html` to land on the curriculum home page. From there, navigate through any of the 7 chapters, or start at **L0** and go in sequence.

The top sticky bar on every chapter page is a 7-step path indicator — click any chapter to jump there.

## Chapters

| # | Title | Teaches | Day |
|---|-------|---------|-----|
| L0 | The brief | Three questions before you start | Day 1 |
| L1 | Understanding data | Translate before you analyze — the glossary | Day 2 |
| L2 | Cleaning data | Four kinds of wrong rows — dedupe/impossibles/nulls/window | Day 2 late afternoon |
| L3 | The right question | Root cause analysis + 5-why | Day 3 |
| L4 | Evidence or theater | Chart magnitude · sample size · prose slop | Day 3 |
| L5 | Finding → recommendation | The four parts of a committing recommendation | Day 3 evening |
| L6 | The container is the fight | Format as function — the one-pager | Day 4 |

## Hosting on GitHub Pages

This bundle is designed to be served statically. To host on GitHub Pages:

1. Create a new repository on GitHub (**private** recommended — see security note below).
2. From the `zero-foundations/` directory:
   ```bash
   git init
   git add .
   git commit -m "Initial: Zero Foundations curriculum v1"
   git branch -M main
   git remote add origin git@github.com:YOUR-USERNAME/YOUR-REPO.git
   git push -u origin main
   ```
3. In the repo Settings → Pages, set:
   - Source: **Deploy from a branch**
   - Branch: **main** / **/ (root)**
4. Wait ~30s for Pages to build. Your site lives at:
   `https://YOUR-USERNAME.github.io/YOUR-REPO/`

Share that URL with your team. Every chapter HTML becomes a deep link:
`https://YOUR-USERNAME.github.io/YOUR-REPO/ZERO-L1-Concept-UnderstandData-v1.html`

## Security note — the Gemini API key

Chapters **L2, L4, L5, L6** make direct browser-to-Gemini API calls for the live Claude Cowork interactions. The API key (`AIzaSy...`) is embedded in each HTML file.

If the GitHub repo is **public**, that key is public. Three ways to handle:

1. **Private repo + Pages** — private GitHub repos can still serve Pages (on Pro/Team/Enterprise plans). Cleanest option for internal sharing.
2. **Rotate the key** — rotate in Google Cloud Console after demo windows close, and set aggressive rate limits on it.
3. **Move to a proxy later** — for production, replace the direct API calls with a call to your own serverless endpoint (Vercel/Cloudflare) that holds the real key server-side. All four chapter JS files have a single `callGemini(...)` function; swap the URL in that function and you're done.

## Directory structure

```
zero-foundations/
├── index.html                                        # landing page
├── ZERO-L0-Concept-CostReduction-v3.html             # 7 chapter HTMLs
├── ZERO-L1-Concept-UnderstandData-v1.html
├── ZERO-L2-Concept-CleanData-v1.html
├── ZERO-L3-Concept-FiveWhy-v3.html
├── ZERO-L4-Concept-EvidenceOrTheater-v1.html
├── ZERO-L5-Concept-FindingToRecommendation-v1.html
├── ZERO-L6-Concept-ContainerIsTheFight-v1.html
├── ZERO-L0-assets/ ... ZERO-L6-assets/               # per-chapter audio
│   └── audio/
│       ├── manifest.json
│       └── *.mp3                                     # pre-generated voiceover
└── README.md
```

## What powers the interactivity

- **Voice narration (Avery):** pre-generated MP3s from ElevenLabs v3. Stored in each chapter's `assets/audio/` folder with a `manifest.json` that maps files to timings.
- **Live AI (Claude Cowork sim):** Gemini 2.5 Flash called directly from browser. System prompts in each HTML pin the model's persona to "Claude Cowork" for the specific scenario.
- **POU mini-games:** deterministic multiple-choice, hardcoded for precise teaching.

## Feedback channel

When your team goes through this, collect feedback on:
- Does each chapter's concept land clearly?
- Do the POU mini-games feel too easy / too hard?
- Does the live Gemini PIP interaction feel natural?
- Are there places where the 7-step path indicator helps vs. clutters?

Track findings in a spreadsheet or Linear — iterate on specific chapters.

## Built with

Claude Cowork · ElevenLabs v3 · Gemini 2.5 Flash-Lite · plain HTML/CSS/JS (no framework).
